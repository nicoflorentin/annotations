crear servidor : 
```js
const http = require('http')
http.createServer()
```
se ejecuta cada vez que el servidor reciba una petición

```js
http.createServer((req, res) => {
	res.writeHead(200, {'Conten-Type': 'text/plain'})
	res.end('Hello from server!')
}).listen(3001, 'localhost')
```
- req : request
- res: response
- encabezados
- status code 200
- 3001 es el puerto

### .listen ( ) : 

http.CreateServer().listen( _port_, _hostname_, _backlog_, _callback_ );
- port : Optional. Specifies the port we want to listen to
- hostname :  Optional. Specifies the IP address we want to listen to
- backlog : Optional. Specifies the max length of the queue of pending connections. Default 511
- callback : Optional. Specifies a function to be executed when the listener has been added

### Status code : 
200 : todo ok
300 
400 : error del cliente
500 : error del servidor

### El servidor responde a la reques con un JSON :
```js
http.createServer((req, res) => {
	res.writeHead(200, {'Conten-Type': 'application/json'})
	res.end(JSON.stringify([{id: 1,name: 'florent'},{id: 2, name: 'florent'}]))
}).listen(3001, 'localhost')
```

### Respuestas condicionales :
```js
http.createServer((req, res) => {
	const {url} = req
	if (url === '/') {
		res.writeHead(200, {'Content-Type': 'text/plain'})
		res.end('Hello!')
	}
	if (url === '/students') {
		res.writeHead(200, {'Conten-Type': 'application/json'})
		res.end(JSON.stringify([{id: 1,name: 'florent'},{id: 2, name: 'florent'}]))
	} else {
		res.writeHead(404)
		res.end()
	}
}).listen(3001, 'localhost')
```

What does res end do in NodeJS?
The res. end() method **ends the current response process**. This method is used to quickly end the response without any data.

### El servidor devuelve un html :
```js
if (url === '/html') {
const html = fs.readFileSync(__dirname + '/src/index.html', 'utf-8')
res.writeHead(200, {'Content-Type': 'text/html'})
return res.end(html)
}
```

### Reeemplazar algo en el html : 
```js
if (url === '/html') {
const html = fs.readFileSync(__dirname + '/src/index.html', 'utf-8')
const nombre = 'Florent'
res.writeHead(200, {'Content-Type': 'text/html'})
return res.end(html.replace('{nombre}', nombre))
}
```

### Tipos de Content-Type : 
1.  Texto plano (Plain text) - text/plain
2.  HTML (Hypertext Markup Language) - text/html
3.  XML (Extensible Markup Language) - application/xml
4.  JSON (JavaScript Object Notation) - application/json
5.  Imágenes JPEG (Joint Photographic Experts Group) - image/jpeg
6.  Imágenes PNG (Portable Network Graphics) - image/png
7.  GIFs animados (Graphics Interchange Format) - image/gif
8.  Archivos de audio MP3 (MPEG Layer-3) - audio/mpeg
9.  Archivos de audio OGG (Ogg Vorbis) - audio/ogg
10.  Archivos de video MP4 (MPEG-4) - video/mp4
11.  Archivos de video WebM (WebM Project) - video/webm
12.  Archivos PDF (Portable Document Format) - application/pdf
13.  Archivos ZIP (Compressed Archive File) - application/zip
14.  Archivos de hojas de cálculo Excel - application/vnd.ms-excel
15.  Archivos de presentaciones PowerPoint - application/vnd.ms-powerpoint

### En caso de error con peticion en React : 

```js
//dentro del server
res.setHeader('Acces-Control-Allow-Origin', '*')
```