## module.exports

```js
// index.js
const {suma} = require('./funciones')

const resultado = suma(num1, num1)
console.log(resultado) // 9
```
```js
/// funciones.js
const suma = (a,b) => a + b
const resta = (a,b) => a - b

module.exports = {
	suma,
	resta
}
```

## export
```js
// index.js
import {suma} from './funciones'

const resultado = suma(num1, num2)
console.log(resultado) // 9
```
```js
// funciones.js
export const suma = (a,b) => a + b
export const resta = (a,b) => a - b
```

## export default
solo se puede hacer un export default por archivo
```js
// index.js
import suma from './funciones'

const resultado = suma(num1, num2)
console.log(resultado) // 9
```
```js
// funciones.js
const suma = (a,b) => a + b

export default suma
```
## Instalar webpack

1- en consola --> npm i webpack webpack-cli
2- Agregar el script : 

![[Pasted image 20230303115652.png]]

3- Creo webpack.config : 
path: la carpeta donde se va a crear
filename: el archivo output (js puro)
![[Pasted image 20230303120203.png]]
4- en consola ---> npm build