### Crear un servidor

se le pasa el puerto a escuchar y una callback opcional :
```js
server.listen(3000, callback() => {
	console.log('server listening on port 3000')
})
```

### Métodos HTTP
```js
server.get()
server.post()
server.put()
server.delete()
```
#### get()
```js
server.get('/route', (request, response) => {
	res.send("I'm the server response message")
})
```

#### post()
**Hace falta usar un middleware** para interpretar el json que enviamos desde front : **TRADUCTOR**
Es para usar el **body como un objeto json**
```js
//MIDDLEWARE
//tiene que estar arriba de todo antes de las rutas
server.use(express.json())
```
luego ejecutamos el handler de la ruta
```js
//solo el método post utiliza el re.body por buena practica
let info = [];
server.post('/posteo', (request, response) => {

	let post = req.body
	info.push(post)
	res.json(info)
})
```
### Routing
![[Pasted image 20230327232659.png]]

### Recibir informacion : 
- Podemos recibir informacion por tres medios :
	- PARAMS
	- QUERY
	- BODY


#### params : 
puedo mandar todas las params que quiera, son obligatorios y los tengo que indicar en la URL
```js
server.get('/route/:id', (request, response) => {
	console.log(req.params)
})
```
#### query
La informacion de la query puede llegar o no, no hace falta que especifique la URL, puedo pasar mas de una query (/users?name=nicolas&&surname=florentin)
```js
// /users?name=nicolas
server.get('/users', (request, response) => {
	console.log(req.query)
})
```
#### body
Hay que usar un middleware para traducir la información, se puede postear un archivo json
```js
let post = req.body
	info.push(post)
	res.json(info)
```

## Middlewares

Una http request puede pasar por una serie de middlewares antes que el router handler de una respuesta

- TRADUCTOR entre el usuario y el servidor

### modularizar con server.use()
los filepath vienen desde server.router

#### server
![[Pasted image 20230328023447.png]]


#### posteo
![[Pasted image 20230328023742.png]]

routerPost es un paquete de rutas

**SIEMPRE SE MODULARIZA CON EL ROUTER**

Hacer un Router para get, otro para post otro para put y otro para delete.

## Morgan (middleware)
nos da informacion de la request que nos hicieron y con que status le respondió el servidor.

npm install morgan
```js
const morgan = require('morgan')
server.use(morgan('dev'))
```
## Permisos CORS

npm install cors
```js
const cors = require('cors')
server.use( cors() )
```

## Esctructura de archivos : 

![[Pasted image 20230329020059.png]]



**/////////////////////////////////////////////////////////////////**



## Apuntes de homework
![[Pasted image 20230327111105.png]]
![[Pasted image 20230327112948.png]]

el .use aplica un middleware
.get lee las rutas y ejecuta
.req tiene los params y la query
.res manda la respuesta de la query
.next es para salir de un middleware, se ejecuta el middleware y con next seguis en la ejecucion. es una callback que apunta a un middleware


## **Repaso de creación de rutas**

Básicamente, la creación de rutas sirve para determinar cómo una aplicación responde a la solicitud de un cliente en una determinada vía de acceso (llamada URI) con un método de solicitud HTTP específico. En otras palabras, lo que vamos a hacer es invocar uno de estos métodos HTTP (especialmente POST, GET, PUT, HEAD y DELETE), utilizando la variable app, para indicarle la acción que queremos realizar y disponer la ruta que queremos para una determinada URI.

Es por esto que la definición de creación de rutas es la siguiente:

```javascript
server.METHOD(PATH, HANDLER);
```

Donde:

-   server es una instancia de express
-   METHOD es un método de solicitud HTTP
-   PATH es la vía de acceso al servidor
-   HANDLER es la función que se ejecuta cuando se hace el direccionamiento a la ruta, siempre recibe como parámetro dos variables, req por request y res por response.

Ejemplos :
```javascript
server.get('/', function (req, res) {
   //Ruta para un GET a /
   res.send('Hola mundo!'); // response "Hola mundo!" en la pagina principal
});
```
### res.body()
Queremos que se envíe con el formato JSON podríamos hacer lo siguiente:
```javascript
server.get('/', function (req, res) {
   var obj = {
      saludo: 'Hola mundo!',
   };
   res.json(obj);
});
```

### res.status()
Ahora supongamos que queremos setear el status de la response como 200 para indicar que la solicitud ha tenido éxito, para eso utilizaremos `res.status()`.

```javascript
server.get('/', function (req, res) {
   res.status(200).send('Hola mundo!');
});
```

### res.body()
Otro punto a tener en cuenta es que `req.body` se usa para tener los parámetros que son enviados por el cliente como parte de un request. Entonces, si por ejemplo quisiera acceder a la propiedad name podría utilizar `req.body.name`.

```javascript
server.post('/', function (req, res) {
   var obj = {
      saludo: 'Hola' + req.body.name,
   };
   res.json(obj);
});
```

### req.query()
Para finalizar si queremos acceder a los parámetros de una consulta utilizaremos `req.query`. Por ejemplo, supongamos que se desea buscar 'toni' realizando un `GET /search?name=toni`, entonces lo que haremos será acceder al parámetro nombre de la query con `req.query.name`.

![[Pasted image 20230404205250.png]]

![[1695704148777.pdf]]