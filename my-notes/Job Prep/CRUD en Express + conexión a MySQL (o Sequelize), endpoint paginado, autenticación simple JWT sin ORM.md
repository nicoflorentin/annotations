# Estructura profesional de API Express + MySQL (SQL nativo) + JWT + paginación

```
project/
├── src/
│   ├── app.js
│   ├── server.js
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   │   └── userController.js
│   ├── routes/
│   │   └── userRoutes.js
│   ├── services/
│   │   └── userService.js
│   ├── repositories/
│   │   └── userRepository.js
│   ├── middlewares/
│   │   └── authMiddleware.js
│   ├── utils/
│   │   └── jwt.js
│   └── models/
│       └── createTables.sql
├── .env
├── package.json
└── README.md
```


### **1️⃣ Configuración de la base de datos (`config/db.js`)**

```js
import mysql from 'mysql2/promise';
import dotenv from 'dotenv';
dotenv.config();

const pool = mysql.createPool({
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASS,
  database: process.env.DB_NAME,
  connectionLimit: 10,
});

export default pool;
```


### **2️⃣ Servidor principal (`server.js`)**

```js
import app from './app.js';
import dotenv from 'dotenv';
dotenv.config();

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`🚀 Server running on port ${PORT}`));
```


### **3️⃣ App principal (`app.js`)**

```js
import express from 'express';
import cors from 'cors';
import userRoutes from './routes/userRoutes.js';

const app = express();
app.use(cors());
app.use(express.json());

app.use('/api/users', userRoutes);

app.get('/', (req, res) => res.send('API Running'));

export default app;
```


### **4️⃣ Repositorio SQL nativo (`repositories/userRepository.js`)**

```js
import pool from '../config/db.js';

export const getAllUsers = async (limit, offset) => {
  const [rows] = await pool.query('SELECT id, name, email FROM users LIMIT ? OFFSET ?', [limit, offset]);
  return rows;
};

export const getUserById = async (id) => {
  const [rows] = await pool.query('SELECT id, name, email FROM users WHERE id = ?', [id]);
  return rows[0];
};

export const createUser = async ({ name, email, password }) => {
  const [result] = await pool.query('INSERT INTO users (name, email, password) VALUES (?, ?, ?)', [name, email, password]);
  return result.insertId;
};

export const updateUser = async (id, { name, email }) => {
  await pool.query('UPDATE users SET name = ?, email = ? WHERE id = ?', [name, email, id]);
};

export const deleteUser = async (id) => {
  await pool.query('DELETE FROM users WHERE id = ?', [id]);
};

export const getUserByEmail = async (email) => {
  const [rows] = await pool.query('SELECT * FROM users WHERE email = ?', [email]);
  return rows[0];
};
```


### **5️⃣ Servicio con lógica (`services/userService.js`)**

```js
import bcrypt from 'bcryptjs';
import jwt from 'jsonwebtoken';
import * as repo from '../repositories/userRepository.js';

export const listUsers = async (page = 1, limit = 10) => {
  const offset = (page - 1) * limit;
  return repo.getAllUsers(limit, offset);
};

export const registerUser = async (data) => {
  const hashed = await bcrypt.hash(data.password, 10);
  return repo.createUser({ ...data, password: hashed });
};

export const loginUser = async (email, password) => {
  const user = await repo.getUserByEmail(email);
  if (!user) throw new Error('User not found');
  const valid = await bcrypt.compare(password, user.password);
  if (!valid) throw new Error('Invalid password');

  const token = jwt.sign({ id: user.id, email: user.email }, process.env.JWT_SECRET, { expiresIn: '1h' });
  return { token };
};
```


### **6️⃣ Controlador (`controllers/userController.js`)**

```js
import * as service from '../services/userService.js';

export const getUsers = async (req, res) => {
  try {
    const { page = 1, limit = 10 } = req.query;
    const users = await service.listUsers(Number(page), Number(limit));
    res.json(users);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
};

export const register = async (req, res) => {
  try {
    const id = await service.registerUser(req.body);
    res.status(201).json({ id });
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
};

export const login = async (req, res) => {
  try {
    const { email, password } = req.body;
    const data = await service.loginUser(email, password);
    res.json(data);
  } catch (err) {
    res.status(401).json({ error: err.message });
  }
};
```


### **7️⃣ Rutas (`routes/userRoutes.js`)**

```js
import { Router } from 'express';
import * as ctrl from '../controllers/userController.js';
import { authMiddleware } from '../middlewares/authMiddleware.js';

const router = Router();

router.get('/', authMiddleware, ctrl.getUsers);
router.post('/register', ctrl.register);
router.post('/login', ctrl.login);

export default router;
```


### **8️⃣ Middleware de autenticación (`middlewares/authMiddleware.js`)**

```js
import jwt from 'jsonwebtoken';

export const authMiddleware = (req, res, next) => {
  const header = req.headers['authorization'];
  if (!header) return res.status(401).json({ error: 'Token missing' });

  const token = header.split(' ')[1];
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch {
    res.status(403).json({ error: 'Invalid token' });
  }
};
```


### **9️⃣ Script SQL (`models/createTables.sql`)**

```sql
CREATE TABLE IF NOT EXISTS users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

### **🔟 Variables `.env`**

```
PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASS=yourpassword
DB_NAME=mydatabase
JWT_SECRET=mysecretkey
```


### **✅ Características:**
- CRUD con SQL nativo (sin ORM)
- Paginación (`?page=1&limit=10`)
- Login/Register con JWT
- Middleware de autenticación
- Arquitectura escalable y limpia
