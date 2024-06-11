https://www.youtube.com/watch?v=pwrv5D2bXJM&list=PLergODdA95kcnpakDg4ShmargckgOVoHH&index=1&ab_channel=codrr

### CLASE 0
```ts
//* CLASE 0
  
// compilar: npx tsx (npm porque no esta instalado a nivel global, ...
// ... no se instala el CLI y la consola no reconoce le comando)
// ejecutar: node ./dist/test.js
const number: number = 2
  
const logData = (number: number): void => {
  console.log(number)
}
```

### CLASE 1
  ```ts
//* CLASE 1 - TIPOS BASICOS
  
let myStringVar: string = "Rodrigo"
myStringVar = "asd"
  
let myBooleanVar: boolean
myBooleanVar = false
  
let myNullVar: null
myNullVar = null
  
let myUndefinedVar: undefined = undefined
  
//---------------------------
// Funciones
  
function myName(string: string): number {
  return Number(string)
}
  
// funcion flecha
const myNameV2 = (name: string): string => {
  return `Hola ${name}`
}
  
//declaramos una variable de tipo funcion para inicializarla mas tarde
let myNameV3: (name: string) => void
myNameV3 = (name) => {
  console.log(name)
}
```

### CLASE 3
```ts
//* CLASE 3 - TIPOS BASICOS 2
  
//Array
  
const names: string[] = []
// declarar con un genérico
const namesV2: Array<string> = []
  
// Object o Records
  
const myObject: Object = {
  name: "Rodri",
}
  
// Record
// el primer elemento es el tipo de la key y el segundo es el tipo del value
const myObjectV2: Record<string, any> = {
  string: "value",
  year: 2024,
  string2: false,
}
  
// Tuplas
  
let myObjectV3: Record<string, string | number>
myObjectV3 = {
  string: "value",
  year: 2024,
  string2: "false",
}
  
// Promesas
  
const myPromise = async (): Promise<string> => {
  return await new Promise((res, _rej) => {
    setTimeout(() => {
      res("hola")
    }, 1000)
  })
}
  
myPromise().then((res) => console.log(res))
  
// Compuestos
  
const myNewObject: { name: string; age: number } = {
  age: 28,
  name: "Rodrigo",
}

```

### CLASE 2
```ts
//* Clase 2 - Intercaces vs Types
  
// se puede declarar varias veces y no da error, se acumulan
interface IProductoBase {}
  
// esto es unico de los types, selectores
type PaymentMethodType = "debito" | "credito" | "efectivo"
  
interface IProductoBase {
  price: number
  paymentMethod: PaymentMethodType
  nameClient: string
}
  
type ProductoBaseType = {
  price: number
  paymentMethod: PaymentMethodType
  nameClient: string
}
  
// Herencia
  
// se puede extender con un type o con una interface
interface Fisica extends IProductoBase {
  productName: string
  clientAdress: string
  quantity: number
}
  
// los "or" en la extension de type son validos ero no para crear una clase de javascript, las clases esperan types estáticos y no dinámicos
// type Virtual = ProductoBaseType | {
type Virtual = ProductoBaseType & {
  templateName: string
  format: "jpg" | "png" | "pdf"
}
  
class ProductoVirtual implements Virtual {
  price: number = 500
  paymentMethod: PaymentMethodType = "efectivo"
  nameClient: string = "Rodrigo"
  templateName: string = "folleto1
  format: "jpg" | "png" | "pdf" = "pdf"
}
  
class ProductoFisico implements Fisica {
  price: number = 500
  paymentMethod: PaymentMethodType = "efectivo"
  nameClient: string = "Rodrigo"
  productName: string = "Folleto"
  clientAdress: string = "Street 1000"
  quantity: number = 1000
}
```

### CLASE 4
```ts
//* CLASE 4 - GENERICOS
// Es una especie de plantilla de codigo mediante la cual podemos aplicar...
// ...un tipo de datos determinado a varios puntos de nuestro codigo
  
interface MyProps<T> {
  myGenericType: T
}
  
interface MyGenericInterface<T, U> {
  myGenericType: T | U
}
  
const example: MyGenericInterface<string, number | boolean> = {
  myGenericType: true,
}
  
// ---------------------------
  
function getValue<T>(value: T) {
  console.log(value)
}
  
getValue<number>(5)
  
const getValueV2 = <T>(value: T) => {
  console.log(value)
}
  
// ---------------------------
  
type MyGenericType<T, U> = {
  myGenericType: T | U
}
  
// ---------------------------
  
class GenericClass<T> {
  protected value!: T
  constructor(value: { new (): T }) {
    this.value = new value()
  }
}
  
class Rodri {
  public name: string = 'Rodri'
  public age: number = 30
}
  
class Maria {
  public name: string = 'Maria'
  public age: number = 24
}
  
class Greet extends GenericClass<Rodri> {
  constructor() {
    super(Rodri)
  }
  public greet(): void {
    console.log(`Hello ${this.value.name}`)
  }
}
```

### CLASE 5
```ts
  
//* Clase 5 - TIPOS CONDICIONALES
  
type Perro = {
  nombrePerro?: string
  edad?: number
  ladra: boolean
}
  
type Gato = {
  nombreGato: string
  edad: number
  trepa: boolean
}
  
type SeleccionAnimal<T> = T extends "perro" ? Perro : Gato
  
function seleccionAnimal<T extends "perro" | "gato">(animal: SeleccionAnimal<T>) {
  console.log(animal)
}
  
seleccionAnimal<"perro">({ ladra: true })
```
### CLASE X
```ts
//* DECORATORS
```

