Perfecto, mirá este ejemplo práctico 👇

Supongamos que tenés una tabla `users` y querés devolver los resultados paginados desde tu API Express.

---

### 🧠 Lógica general del paginado

Querés algo tipo:

```
GET /users?page=2&limit=10
```

Que te devuelva la **segunda página** de usuarios, **10 por página**.  
En SQL, eso se hace con `LIMIT` y `OFFSET`:

```sql
SELECT * FROM users
ORDER BY id
LIMIT 10 OFFSET 10;
```

El `OFFSET` se calcula así:

```
OFFSET = (page - 1) * limit
```

---

### 💻 Ejemplo completo con Express y PostgreSQL/MySQL

```js
import express from "express";
import mysql from "mysql2/promise"; // o 'pg' si usás PostgreSQL

const app = express();

// Pool de conexiones para rendimiento
const pool = mysql.createPool({
  host: "localhost",
  user: "root",
  password: "password",
  database: "testdb",
  connectionLimit: 10,
});

app.get("/users", async (req, res) => {
  try {
    // Parámetros de paginado
    const page = parseInt(req.query.page) || 1;
    const limit = parseInt(req.query.limit) || 10;
    const offset = (page - 1) * limit;

    // Consulta de datos
    const [rows] = await pool.query(
      `SELECT id, name, email FROM users ORDER BY id LIMIT ? OFFSET ?`,
      [limit, offset]
    );

    // Conteo total para calcular páginas
    const [[{ total }]] = await pool.query(`SELECT COUNT(*) AS total FROM users`);

    res.json({
      data: rows,
      meta: {
        page,
        limit,
        total,
        totalPages: Math.ceil(total / limit),
      },
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "Error interno del servidor" });
  }
});

app.listen(3000, () => console.log("Server running on http://localhost:3000"));
```

---

### 📊 Ejemplo de respuesta

```json
{
  "data": [
    { "id": 11, "name": "Lucía", "email": "lucia@mail.com" },
    { "id": 12, "name": "Martín", "email": "martin@mail.com" }
  ],
  "meta": {
    "page": 2,
    "limit": 10,
    "total": 53,
    "totalPages": 6
  }
}
```

---

### ⚙️ Tips pro

- Siempre hacé `ORDER BY id` o algún campo estable para evitar resultados inconsistentes.
    
- En datasets muy grandes, el `OFFSET` puede volverse lento → se puede optimizar con **paginación basada en cursores** (`WHERE id > last_id`).
    
- Devolvé metadata (`total`, `totalPages`) para que el frontend pueda renderizar la paginación.
    

---

¿Querés que te muestre cómo sería el mismo ejemplo pero con **paginación por cursor (más eficiente)**?