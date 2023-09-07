
como configurar variables de entorno

instalar dotenv : 
```bash
npm install dotenv
```

ejecutar dotenv y su metodo config : 
```js
require('dotenv').config()
const PORT = process.env.PORT || 3001
```

configurar archivo .env : 
```env
(.env file en el root del proyecto)
PORT=3002
```
