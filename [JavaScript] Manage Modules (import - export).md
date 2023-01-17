---
tags: [JavaScript]
title: '[JavaScript] Manage Modules (import - export)'
created: '2022-02-15T23:33:30.523Z'
modified: '2022-09-13T03:17:17.851Z'
---

# [JavaScript] Manage Modules (import - export)

Especificar que el script es de tipo módulo:

```html
<script src='./folder/script.js' type="module"></script>
```

Para que funcione el type module tenes que configurar un **live server con npm**. No se pueden utilizar módulos utilizando el protocolo "file://" (en el navegador)

npm i live-server
live-server "folder"

Exportar la variable "variable" desde module.js
```js
export default variable
```

Exportar varias variables desde module.js
```js
export { variable1 , variable2 }
```

```js
import { variable1 , variable2 } from './folder/module.js'
```

```js
import variable from './folder/module.js'
```

```js
import variable , { variable1, variable2 } from './folder/module.js'
```

export default solo puede utilzarse una sola vez por script

## Importar todo lo que hay dentro del script :

```js
import * from './module.js'
```

Importar todo usando un alias, exporta un objeto con las variables en forma de propiedades de objeto: 

```js
import * as Modulo from './module.js'

Modulo.variable
Modulo.variable1
Modulo.variable2
```



