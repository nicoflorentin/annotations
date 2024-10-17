Instalaremos json-server en nuestro proyecto...

```js
npm install json-server --save-dev
```

y agregaremos la siguiente línea a la parte de _scripts_ del archivo _package.json_

```js
"scripts": {
  "server": "json-server -p3001 --watch db.json",
  // ...
}
```

Ahora iniciemos json-server con el comando _npm run server_.