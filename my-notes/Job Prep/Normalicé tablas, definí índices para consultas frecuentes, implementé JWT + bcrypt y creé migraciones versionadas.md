### 🧩 1. **Normalicé tablas**

Esto significa que **reorganizaste la base de datos** para evitar duplicar información y mejorar la consistencia.  
Por ejemplo, en lugar de tener una tabla “usuarios” donde también guardás los nombres de sus roles, lo separás:

```sql
-- Tabla de usuarios
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  password_hash TEXT,
  role_id INT REFERENCES roles(id)
);

-- Tabla de roles
CREATE TABLE roles (
  id SERIAL PRIMARY KEY,
  name VARCHAR(50)
);
```

Así, si mañana querés cambiar el nombre del rol, lo hacés una sola vez en `roles`, no en todos los usuarios.  
➡️ **Beneficio:** menos redundancia y más integridad de datos.

---

### ⚙️ 2. **Definí índices para consultas frecuentes**

Si notás que muchas queries filtran por `email` o `created_at`, conviene crear índices para que las búsquedas sean más rápidas:

```sql
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_created_at ON users(created_at);
```

➡️ **Ejemplo real:** cuando hacés login (`SELECT * FROM users WHERE email = '...'`), el índice acelera muchísimo la búsqueda.

---

### 🔐 3. **Implementé JWT + bcrypt**

Esto cubre **autenticación y seguridad**.

- **bcrypt:** se usa para **encriptar contraseñas** antes de guardarlas.
    
- **JWT (JSON Web Token):** se usa para **mantener sesiones seguras** sin guardar el estado en el servidor.
    

```js
import bcrypt from "bcrypt";
import jwt from "jsonwebtoken";

// Registro
const hashedPassword = await bcrypt.hash(password, 10);
await db.query("INSERT INTO users (email, password_hash) VALUES ($1, $2)", [email, hashedPassword]);

// Login
const user = await db.query("SELECT * FROM users WHERE email = $1", [email]);
const valid = await bcrypt.compare(password, user.password_hash);
if (!valid) throw new Error("Credenciales inválidas");

const token = jwt.sign({ id: user.id }, process.env.JWT_SECRET, { expiresIn: "1h" });
res.json({ token });
```

➡️ **Beneficio:** las contraseñas nunca se guardan en texto plano y el token permite autenticarse sin guardar sesión en memoria.

---

### 🧱 4. **Creé migraciones versionadas**

En lugar de crear tablas “a mano” en SQL, se crean **migraciones** con herramientas como **Knex**, **Sequelize** o **TypeORM**.  
Cada migración representa una “versión” del esquema de tu base de datos.

Por ejemplo, con Knex:

```bash
npx knex migrate:make create_users_table
```

```js
// migrations/20231006123456_create_users_table.js
export function up(knex) {
  return knex.schema.createTable("users", (table) => {
    table.increments("id").primary();
    table.string("email").unique().notNullable();
    table.string("password_hash").notNullable();
  });
}

export function down(knex) {
  return knex.schema.dropTable("users");
}
```

Después aplicás los cambios con:

```bash
npx knex migrate:latest
```

➡️ **Beneficio:** podés mantener un historial de cambios y compartirlo con el equipo o el entorno de producción sin errores manuales.

---

### 🧠 En resumen

|Tarea|Qué hace|Beneficio|
|---|---|---|
|Normalización|Divide tablas en entidades lógicas|Evita duplicar datos|
|Índices|Crea accesos rápidos a columnas|Mejora rendimiento|
|JWT + bcrypt|Maneja login seguro|Protege credenciales|
|Migraciones versionadas|Versiona los cambios en la DB|Facilita despliegue y trabajo en equipo|
