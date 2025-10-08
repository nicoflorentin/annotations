Perfecto 😎, te armo una estructura **profesional y escalable** para manejar autenticación JWT + control de roles en **Express** con buenas prácticas modernas.

---

## 🧱 Estructura de carpetas

```bash
src/
├── app.js
├── server.js
├── config/
│   └── jwt.js
├── middlewares/
│   ├── authMiddleware.js
│   └── roleMiddleware.js
├── controllers/
│   └── userController.js
├── services/
│   └── authService.js
├── routes/
│   ├── authRoutes.js
│   └── userRoutes.js
└── utils/
    └── responseHandler.js
```

---

## ⚙️ `config/jwt.js`

Centralizás la generación y verificación del token:

```js
import jwt from 'jsonwebtoken';

const SECRET = process.env.JWT_SECRET || 'supersecret';

export const generateToken = (user) => {
  return jwt.sign(
    {
      id: user.id,
      email: user.email,
      role: user.role,
    },
    SECRET,
    { expiresIn: '1h' }
  );
};

export const verifyToken = (token) => {
  return jwt.verify(token, SECRET);
};
```

---

## 🧩 `middlewares/authMiddleware.js`

Verifica si el usuario está autenticado:

```js
import { verifyToken } from '../config/jwt.js';

export const authenticate = (req, res, next) => {
  const header = req.headers.authorization;
  if (!header) return res.status(401).json({ message: 'Token requerido' });

  const token = header.split(' ')[1];
  try {
    const decoded = verifyToken(token);
    req.user = decoded; // guarda el user en el request
    next();
  } catch (err) {
    return res.status(401).json({ message: 'Token inválido o expirado' });
  }
};
```

---

## 🧰 `middlewares/roleMiddleware.js`

Restringe acceso según rol:

```js
export const authorize = (...roles) => {
  return (req, res, next) => {
    if (!roles.includes(req.user.role)) {
      return res.status(403).json({ message: 'Acceso denegado' });
    }
    next();
  };
};
```

---

## 🔐 `services/authService.js`

Acá iría la lógica de login (comparar password, etc.):

```js
import bcrypt from 'bcrypt';
import { generateToken } from '../config/jwt.js';
import { getUserByEmail } from '../repositories/userRepository.js';

export const loginUser = async (email, password) => {
  const user = await getUserByEmail(email);
  if (!user) throw new Error('Usuario no encontrado');

  const valid = await bcrypt.compare(password, user.password);
  if (!valid) throw new Error('Contraseña incorrecta');

  const token = generateToken(user);
  return { token, user };
};
```

---

## 🚪 `routes/userRoutes.js`

Protegés rutas según rol:

```js
import express from 'express';
import { authenticate } from '../middlewares/authMiddleware.js';
import { authorize } from '../middlewares/roleMiddleware.js';
import { getAllUsers } from '../controllers/userController.js';

const router = express.Router();

router.get('/', authenticate, authorize('admin'), getAllUsers);

export default router;
```

---

## 📦 `controllers/userController.js`

```js
export const getAllUsers = async (req, res) => {
  // si llegás acá, sos admin
  const users = [{ id: 1, name: 'Nico', role: 'admin' }];
  res.json(users);
};
```

---

## 🧠 Flujo completo

1. El usuario hace **login** → se genera un JWT con el `role`.
    
2. En las rutas privadas, se pasa `Authorization: Bearer <token>`.
    
3. El middleware `authenticate` valida el token y mete `req.user`.
    
4. El middleware `authorize` controla si el rol es válido para esa acción.
    

---

¿Querés que te agregue cómo guardar _refresh tokens_ y renovar el JWT automáticamente cuando expira (para sesiones largas)?