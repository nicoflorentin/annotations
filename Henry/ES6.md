## let var y const

las variables de var tienen alcance de **contexto de ejecucion**
las variables de let y const tienen **alcance de llaves**. Existen unicamente dentro de las llaves donde fueron declaradas.

var se puede redeclarar
var numero = 2
var numero = 5
console.log(numero) // 5

let y const no se pueden redeclarar

## arrow functions y .this

![[Pasted image 20230301115139.png]]

con funciones comunes no pueden tomar el this del objeto **bob**
las arrow function hace auto bind y sabe que fue definida en el objeto **bob**


## Spread

![[Pasted image 20230301130515.png]]

Se pueden modificar el valor de las propiedades del objeto que copio, **pisa los valores anteriores.**