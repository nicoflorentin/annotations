# 1) Promesas y `async`/`await` (qué son y buenas prácticas)

- **Promesa**: un objeto que representa una operación asíncrona (pendiente → resuelta/rechazada).
    
- **`async`/`await`**: azúcar sintáctica sobre promesas. `await` pausa la función `async` hasta que la promesa se resuelva o rechace — facilita leer código asíncrono secuencial.
    

Ejemplo típico en repositorio (MySQL con `mysql2/promise`):

```js
// repositories/userRepository.js
import pool from '../config/db.js';

export async function getUserById(id) {
  const [rows] = await pool.query('SELECT id, name, email FROM users WHERE id = ?', [id]);
  return rows[0]; // undefined si no existe
}
```

**Pitfalls comunes**

- Olvidar `await` => la función devuelve una Promise en lugar del valor.
    
- No propagar errores (no `throw` o no `next(err)`) → rejections no manejadas.
    
- Mezclar callbacks y promesas sin control → race conditions.
    

**Qué decir en la entrevista:** “Uso `async/await` para claridad y manejo centralizado de errores; me aseguro de `await` todo y propagar errores hacia el middleware de errores.”

---

# 2) Manejo de errores en Express (arquitectura y patterns)

- Express distingue errores síncronos y asíncronos. Para asíncronos, si `throw` dentro de `async` no lo atrapás, necesitás pasar el error al `next(err)` o usar un wrapper.
    
- Middleware de error tiene firma `(err, req, res, next)` — es EL lugar para formatear respuesta y loggear.
    

**Wrapper para evitar try/catch repetidos**

```js
// utils/asyncHandler.js
export const asyncHandler = (fn) => (req, res, next) => {
  Promise.resolve(fn(req, res, next)).catch(next);
};
```

Uso:

```js
router.get('/', asyncHandler(async (req, res) => {
  const users = await userService.listUsers();
  res.json(users);
}));
```

**Middleware de errores (ejemplo práctico)**

```js
export default function errorHandler(err, req, res, next) {
  console.error(err); // en prod mandar a logger (winston / sentry)
  if (err.code === 'ER_DUP_ENTRY') {
    return res.status(409).json({ error: 'Registro duplicado' });
  }
  const status = err.status || 500;
  const message = process.env.NODE_ENV === 'production' && status === 500
    ? 'Internal Server Error' : err.message;
  res.status(status).json({ error: message });
}
```

**Qué enfatizar en la entrevista:** “Centralizo la lógica de errores, traduzco errores DB a códigos HTTP útiles (409/400/404) y no devuelvo stack en producción.”

---

# 3) Pooling en MySQL (por qué y cómo usarlo)

**Por qué usar pool**:

- Crear una conexión por request es caro. Un _pool_ mantiene conexiones reutilizables.
    
- Controla el número máximo de conexiones al DB y evita saturarlo.
    

**Crear pool (mysql2/promise):**

```js
import mysql from 'mysql2/promise';
const pool = mysql.createPool({
  host: 'localhost',
  user: 'root',
  password: 'pw',
  database: 'mydb',
  waitForConnections: true,
  connectionLimit: 10, // ajustar según CPU/RAM y max_connections de MySQL
  queueLimit: 0
});
export default pool;
```

**Uso simple (consulta única):**

```js
const [rows] = await pool.query('SELECT * FROM users WHERE id = ?', [id]);
```

**Uso para transacciones (obteniendo conexión del pool):**

```js
const conn = await pool.getConnection();
try {
  await conn.beginTransaction();
  await conn.query(...);
  await conn.commit();
} catch (err) {
  await conn.rollback();
  throw err;
} finally {
  conn.release();
}
```

**Mejor práctica:** nunca crear pools por request; crear pool singleton por proceso. Ajustar `connectionLimit` considerando que cada instancia del servicio tendrá su propio pool.

**Qué decir en la entrevista:** “Configuro pool singleton y cuido `release()` para evitar leaks; si estamos en K8s, ajusto pool por réplica y reviso `max_connections` en MySQL.”

---

# 4) Índices (qué son, cuándo y cómo)

- Índices aceleran búsquedas (WHERE, JOIN, ORDER BY, GROUP BY). MySQL usualmente usa **B-tree** para índices generales.
    
- **Índice simple**: `CREATE INDEX idx_email ON users(email);`
    
- **Índice único**: `CREATE UNIQUE INDEX ux_email ON users(email);`
    
- **Índice compuesto**: `CREATE INDEX idx_orders_user_created ON orders(user_id, created_at);`
    

**Regla del prefijo izquierdo (leftmost):**

- Un índice compuesto `(a, b, c)` puede usarse para consultas que filtren por `a`, `a,b`, o `a,b,c` — no por `b` solo.
    

**Covering index:**

- Si el índice contiene todas las columnas necesarias para la consulta, MySQL puede resolverla solo con el índice (mejor performance).
    

**Cuándo NO indexar:**

- Columnas con muy baja cardinalidad (ej: boolean) no siempre mejoran, y cada índice encarece `INSERT/UPDATE/DELETE`.
    

**Comandos útiles:**

- `EXPLAIN SELECT ...` — ver si se usa índice.
    
- `SHOW INDEX FROM users;` — ver índices existentes.
    

**Qué decir en la entrevista:** “Indexo columnas usadas en WHERE/JOIN/ORDER BY, uso EXPLAIN, y evito sobre-indexar para no penalizar writes.”

---

# 5) JOINs (tipos y buenas prácticas)

- **INNER JOIN**: devuelve filas con coincidencia en ambas tablas.
    
- **LEFT JOIN**: devuelve todas de la izquierda y coincidencias de la derecha (si no hay, NULL).
    
- **RIGHT JOIN**: simétrico de LEFT.
    
- **CROSS JOIN**: producto cartesiano (rara vez usado).
    

Ejemplo:

```sql
SELECT o.id, o.total, u.name
FROM orders o
INNER JOIN users u ON o.user_id = u.id
WHERE u.active = 1
ORDER BY o.created_at DESC
LIMIT 20;
```

**Consejos:**

- Asegurate que las columnas usadas en `ON`/`WHERE` estén indexadas (`orders.user_id`, `users.id`).
    
- Evitá `SELECT *` en joins grandes — pedir sólo las columnas necesarias.
    
- Para evitar N+1 (p. ej. por cada usuario pedir sus órdenes en un loop), preferí un `JOIN` o `IN (...)` con una sola query.
    

**Qué decir en la entrevista:** “Para listados con relaciones uso JOINs bien indexados; para cargas enormes uso paginación por keyset.”

---

# 6) Transacciones (ACID, código y patrones)

**ACID**:

- **A**tomocity: todo o nada.
    
- **C**onsistency: mantiene reglas de integridad.
    
- **I**solation: transacciones no interfieren (niveles de aislamiento).
    
- **D**urability: cambios persistentes tras commit.
    

**Niveles de aislamiento** (MySQL InnoDB por defecto: `REPEATABLE READ`):

- `READ UNCOMMITTED`: permite dirty reads.
    
- `READ COMMITTED`: evita dirty reads.
    
- `REPEATABLE READ`: evita non-repeatable reads (default MySQL).
    
- `SERIALIZABLE`: el más estricto, puede reducir concurrencia.
    

**Ejemplo real: transferencia entre cuentas (evitar race conditions)**

```js
const conn = await pool.getConnection();
try {
  await conn.beginTransaction();

  // bloquear filas para evitar double-spend
  const [fromRows] = await conn.query('SELECT balance FROM accounts WHERE id = ? FOR UPDATE', [fromId]);
  const [toRows]   = await conn.query('SELECT balance FROM accounts WHERE id = ? FOR UPDATE', [toId]);

  if (fromRows[0].balance < amount) throw new Error('Insufficient funds');

  await conn.query('UPDATE accounts SET balance = balance - ? WHERE id = ?', [amount, fromId]);
  await conn.query('UPDATE accounts SET balance = balance + ? WHERE id = ?', [amount, toId]);

  await conn.commit();
} catch (err) {
  await conn.rollback();
  throw err;
} finally {
  conn.release();
}
```

**Deadlocks & retries**

- Si se detecta `ER_LOCK_DEADLOCK`, reintentar la transacción con backoff exponencial (y limite de intentos).
    
- Mantener transacciones lo más cortas posibles (evitar operaciones externas dentro de la tx).
    

**Qué decir en la entrevista:** “Para operaciones críticas uso `SELECT ... FOR UPDATE`, manejo `rollback()` en `catch`, y reintentos ante deadlocks.”

---

# 7) Seguridad y robustez (prácticas relacionadas)

- **Prepared statements / parámetros** (`?`) — evita SQL injection.
    
- Validar y sanitizar inputs (Joi / express-validator).
    
- No devolver errores DB crudos en producción.
    
- Manejar códigos específicos: `ER_DUP_ENTRY` → 409, validación → 400, no encontrado → 404.
    
- Monitoreo: métricas de latencia y tasa de errores, alertas en picos de conexiones.
    

---

# 8) Performance y paginación (tips prácticos)

- **Paginación offset** (`LIMIT 20 OFFSET 1000`) es simple pero lento en offsets grandes. Alternativa: **keyset pagination** (usar `WHERE id < lastId ORDER BY id DESC LIMIT 20`).
    
- Evitá `COUNT(*)` en tablas muy grandes en cada request (usar estimaciones o caché si se necesita).
    
- Usá `EXPLAIN` y `slow_query_log` para identificar queries lentas.
    

---

# 9) Resumen rápido para la entrevista (frases útiles)

- “Uso `async/await` + wrapper `asyncHandler` para propagar errores consistentemente.”
    
- “Pool singleton por proceso, `connectionLimit` ajustado según réplicas y `max_connections` del servidor.”
    
- “Indexo columnas de JOIN/WHERE/ORDER BY, uso EXPLAIN para validar y evito sobre-indexar.”
    
- “Para operaciones multi-step críticas uso transacciones y `SELECT ... FOR UPDATE` y manejo deadlocks con retries.”
    
- “Siempre consultas parametrizadas (`?`) y validación de inputs.”