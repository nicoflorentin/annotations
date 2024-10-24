### Local modules : 

#### CommonJs
Es un estandar de como debe estructurarse y compartirse un módulo.

```js
// in index.js
require('./add.js)
console.log('Hello from index.js')
// la funcion require agrega el modulo add.js al index.js

//output
//3
//Hello from index.js
```

- En nodejs **cada archivo es un módulo que esta aislado** por default
- Para cargar un módule en otro archivo usar la uncion **require**
- Cuando se ejecuta el index.js cada módulo también se ejecuta
- Si el archivo que requerimos es un archivo javascript, **podemos obviar la extensión y node se encarga de interpretarlo**

### Module exports [module.exports = var --> require ('./file')]: 

Export a function :

```js
const add = (a, b) => {
  return a + b;
}
module.exports = add 
//esto es un default export donde no importa con que nombre la define el modulo que importa la función.

// in index.js
const add = require ('./add')
// la constante puede tener cualquier nombre
```

Este es la funcionalidad de import y export que ofrece CommonJs

### Module Scope : 

```js
//batman.js
const superhero = 'batman'
console.log(superhero)

//superman.js
const superhero = 'superman'
console.log(superhero)

//index.js
require('./batman')
require('./superman')
```

- Cada módulo de node tiene su propio scope, superhero no genera conflictos
- Antes de que el codigo de un modulo se ejecute, nodejs lo encierra con un function wrapper que provee module scope

### Module Wrapper : 

node js inyecta parámetros en las funciones para su funcionamiento : 

```js
(function(exports, require, module, __filename, __dirname){
  const superHero = 'batman';
  console.log(superhero)
})
```

### Module Catching : 

```js
//super-hero.js
class SuperHero {
  constructor(name) {
    this.name = name
  }
  getName() {
    return this.name
  }
  setName() {
    this.name = name
  }
}

module.exports = new SuperHero('batman')

//index.js
const superHero = require('./super-hero)
console.log('superHero.setName('superman'))

const newSuperHero = require('./super-hero')
console.log(newSuperHero.getName)
//output : superman
// node recuerda que el modulo super-hero ya fué importado y trae lo que guardó (**module catching**)
```

### Module Import Export Patterns : 

#### 1st Pattern :
```js
//match.js
const add = (a, b) => {
  return a + b;
};
module.exports = add

// index.js
const add = require('./math')
console.log(add(2, 3))

```

#### 2nd Pattern :
```js
//match.js
module.exports = (a, b) => {
  return a + b;
};

// index.js
const add = require('./math')
console.log(add(2, 3))
```

#### 3rd Pattern : 
```js
//match.js
const add = (a, b) => {
  return a + b;
};
const subtract = (a, b) => {
  return a - b;
}
module.exports = {
  add: add,
  subtract: subtract
} // tambien puede usarse DESTRUCTURING

// index.js
const math = require('./math')
console.log(math.add(2, 3))
console.log(math.subtract(2, 3))

//o usando destructuring
const math = require('./math')
const { add, subtract } = math

console.log(add(2, 3))
console.log(subtract(2, 3))
```

#### 4th Pattern : 
```js
//match.js
module.exports.add = (a, b) => {
  return a + b;
};
module.exports.subtract = (a, b) => {
  return a - b;
}
```

#### 5th Pattern : 
```js
//match.js
exports.add = (a, b) => {
  return a + b;
};
exports.subtract = (a, b) => {
  return a - b;
}
```

### ES Modules :

#### CommonJs:
- Cada archivo es tratado como un módulo
- Variables funciones y clases no son accesibles por otros archivos por default
- Se necesita especificarle al sistema de modulos qué partes del codigo son exportados a través de module.exports o exports
- Para importar codigo a un archivo usar funcion require()

#### ES Modules :
- Cuando nodejs fue creado, javascript no tenia un sistema de módulos propio
- Nodejs uso CommonJS como su sistema de modulos predefinido
- **En ES2015 javascript tuvo su sistema de modulos estandarizado como parte del lenguaje**
- El sistema de módulos se llama :
  - EcmaScript Modules
  - ES Modules
  - ESM

#### Cómo funcionan los ES Modules :

#### 1st Pattern : 
```js
//math-esm.mjs
const add = (a, b) => {
  return a + b;
}
export default add
```

```js
//main.mjs
import add from './math-esm.mjs'
console.log(add(5, 5))
```

#### 2nd Pattern :
```js
//math-esm.mjs
export default (a, b) => {
  return a + b;
}

```

```js
//main.mjs
import add from './math-esm.mjs'
console.log(add(5, 5))
```

#### 3rd Pattern :
```js
//math-esm.mjs
const add = (a, b) => {
  return a + b;
}
const subtract = (a, b) => {
  return a - b;
}
export default { add, subtract }
```

```js
//main.mjs
import math from './math-esm.mjs'
const { add, subtract } = math

console.log(add(5, 5))
console.log(subtract(5, 5))
```

#### 4th Pattern : 

```js
//math-esm.mjs
export add = (a, b) => {
  return a + b;
}
export subtract = (a, b) => {
  return a - b;
}
```

```js
//main.mjs
import * as math from './math-esm.mjs'
const { add,subtract } = math
// or
import { add, subtract } from './math-esm.mjs'

console.log(add(5, 5))
console.log(subtract(5, 5))
```

- **Si es un default export, le podemos asignar cualquier nombre a la variable**
- **Si es un named export, el nombre debe ser el mismo**

### Importing JSON and Watch Mode :
- Javascript object notation
- Un formato de intercambio de informacion usado por los servidores web

```json
//data.json
{
  "name": "Bruce Wayne"
  "adress": {
    "street": "Wayne Manor",
    "city": "Gotham"
  }
}

//index.js
const data = require("./data.json")
console.log(data)

//si es un .json se puede o no especificar la extensión
```
**aunque node primero busca extensiones .js y luego busca las .json**
**se recomienda siempre especificar la extensión .json**

#### Watch Mode :
En la consola :
$node --watch index

**El Watch Mode monitorea constantemente los cambios en el archivo**

### Built In Modules : 
- Modulos integrados en nodejs
- Tambien llamados core modules
- Hay que importar el modulo antes de usarlo : 
  - path
  - events
  - fs
  - stream
  - http

### Path Module :
El modulo Path provee herramientas para **manipular archivos y rutas de directorios**
Tiene 14 propiedades y métodos

```js
//index.js
const path = require('node:path')
```

**complete...**

