- instalar express nodemos y morgan
- configurar script para nodemon index.js
- index.js como root del npm start, cuando se ejecuta index necesitamos que se levante el servidor
- hacer carpeta src metemos server.js o app.js
- en el server instanciamos express y creamos el servidor
- en index importamos app y hacemos
```js
const PORT = 3001
app.listen(PORT, ()=>{server lsitening})
```
- en app : 
```js
const morgan = require('morgan')
const cors = require('cors')
const express = require('express')


app.use(morgan('dev'))
app.use(express.json()) //para que los bodys de las request se tranformen en javascript. originalmente no vienen en javascript object
app.use(cors())
module.export = app
```

```js
const myMiddleware = (req, res, next) => {
	cnosole.log('este es mi middleware')
	next() //para que la request siga su camino por el servidor y no queda atrapada en el middleware
}
app.use(myMiddleware) // op: Este es mi middleware (en consola)
```

- cuando llega la request quiero que vaya a un router

USERS : 
- GET /users que me responda con todos los usuarios, salvo que reciba una query 'name', en cuyo caso me filtra por nombre
- GET /users/:id que me responda con el usuario con el id
- GET /users/phone
- POST /users que crea un nuevo usuario
- PUT /users que recibe un id por param y recibe por body los datos nuevos del usuario
- DELETE /users/:id que elimina el usuario por id

CARPETA ROUTES (HANDLERS)

- routes.js o users.routes.js
 ```JS
 const {Router} = require('express')
 const usersRouter = Router()
 ```
 - importar el router en app
 - los handlers son los que manejan la logica de los endpoint
 ```js
 // en app.js
app.use('/users', usersRouter)
app.use('/post', postsRouter)
app.use('*', (req, res)=> {
	res.status(404).json({error: 'Not found'})
})
```
 ```JS
 // /routes/post.router.js
 const {Router} = require('express')
 const postsRouter = Router()
 ```
 users.router
```js
// /routes/users.routerouter.js
// HANDLERS

const getUsers = require ('../controllers/getUsers')

users.router.get('/', (req, res) => {
	const users = getUsers()
	res.status(200).json(users) 
})
 //siempre lo mas especifico va arriba
users.router.get('/phone', (res, req) => {
	res.send()
})

users.router.get('/:id', (req, res) => {
	res.send()
})

users.router.post('/', (req, res) => {
	res.send()
})

users.router.put('/:id', (res, req) => {
	res.send()
})

users.router.delete('/:id', (res, req) => {
	res.send()
})

```

Carpeta controllers
```js
// /controllers/getUsers.js

const data = require('../utils.data')

const getUsers = () => {
	return data
}
```

LOS TRY CATCH VAN EN LOS HANDLERS DE LAS RUTAS

En caso que sean obligatorios 3 datos de 5
![[Pasted image 20230330112356.png]]

![[Pasted image 20230330114058.png]]