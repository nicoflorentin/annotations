https://www.youtube.com/watch?v=fUgxxhI_bvc&ab_channel=midulive

### Tipar funciones
```ts
function saludar({name, age} : {name: string, age: number}): string {
	return age >= 18
		? `${name} es mayor de edad`
		: `${name} es menor de edad`
}

function sumar = (a: number, b:number): number => {
	return a + b
}

function restar: (a: number, b:number)=> number = (a, b) {
	return a - b
}
```

### Usar funciones como parametros
```ts
const sayHi = (fn: (name:string) => void) => {
	return fn('Miguel')
}

sayHiuFromFunction((name) => {
console.log(``Hola ${name}`)
})
```

### Void / Never
- Never : nunca va a devolver un valor
- Void : puede devolver un valor pero este se ignora
```ts
function throwError(message: string): never {
	throw new Error(message)
}
```


### Inferencia de funciones anonimas segun el contexto
```ts
const avengers = ['spider','hulk','cat']
// ya sabe que avenger es un string por hacerle un foreach a un array de strings
avengers.forEach((avenger)=> avenger.toUpperCase())
```

### Type alias
```ts
type Hero = {
	name: string
	age: number
}

function createHero(name: string, age: number): Hero {
	return {name, age}
}

function createHero(hero: Hero): Hero {
	const {name, age} = hero
	return {name, age}
}
```
### Optional properties (?)
```ts
type Hero = {
	// readonly es solo lectura, no se puede modificar
	readonly id?: number
	name: string
	age: number
	isActive?: boolean
}

function createHero(hero: Hero): Hero {
	const {name, age} = hero
	return {name, age, isActive: true}
}

```

### Union types
```ts
type HeroPowerScale = 'planetary' | 'galactic' | 'universal'
let ann: number | string
let ann: number | 'string'
```

### Intersection types
```ts
type HeroBasicInfo = {
name: string
age: number
}

type HeroProperties = {
	readonly id?: number
	isActive?: boolean
	powerscale?: 'planetary' | 'galactic' | 'universal'
}

type Hero = HeroBasicInfo & HeroProperties
```

### Type indexing
```ts
type HeroProperties = {
	isActive?: boolean
	address: {
		planet: string
		city: string
	} 
}

const addressHero: HeroProperties['address'] = {
	planet: 'Earth',
	city: 'Madrid'
}
```

### Type from value
```ts
type address = {
	planet: string
	city: string
}

type Address = typeof address

const addressTwitch: Address = {
	planet: 'Mars',
	city: 'Twitch'
}
```

### Type from function return (ReturnType)
```ts
function createAddress() {
	return {
		planet: 'Tierra',
		city: 'Barcelona'
	}
}

type Address = ReturnType<typeof createAddress>
```

### Arrays
```ts
const languages: (string | number)[] = []
languages.push(2)
languages.push('string)
languages.push(3)

type HeroBasicInfo = {
	id?: number
	name: string
	age: number
}

const herosWithBasicInfo: HeroBasicInfo[] = []

// ARRAY DE ARRAYS
type CellValue = 'X' | 'O' | '' 
type GameBoard = [
	[CellValue,CellValue,CellValue],
	[CellValue,CellValue,CellValue],
	[CellValue,CellValue,CellValue]
]

const gameBoard: GameBOard = [
	['X','X','O'],
	['X','O','O'],
	['X','X','O']
]
```

### Tuples
```ts
type State = [string, (newName: string)=>void]
const [hero, setHero]: State = useState('thor')

type RGB = [number, number, number]
```

### Enums

```ts
enum ERROR_TYPES {
	NOT_FOUND,
	UNAUTHORIZED,
	FORBIDDEN = 'forbidden'
}

// esto compila con menos codigo
const enum ERROR_TYPES {
	NOT_FOUND,
	UNAUTHORIZED,
	FORBIDDEN
}

function mostrarMensaje(tipoDeError: ERROR_TYPES) {
	if (tipoDeError === ERROR_TYPES.NOT_FOUND) {
		console.log('No se encuentra el recurso')
	} else if {
		// (...)
	}
}

```

### Aserciones de tipos
```ts
// Forma buena de validar tipos
const canvas = document.getElementById('span')
if(canvas instanceof HTMLCanvasElement) {
	const ctx = canvas.getContext('2d')
}

//forma mala haciendo asercion de tipos
const canvas = document.getElementById('span')
if(canvas =! null) {
	const ctx = (canvas as HTMLCanvasElement).getContext('2d')
}
```

### Fetching de datos
```ts
const API_URL = 'HTTPS:... ...'
const response = await fetch(API_URL)

// crear los tipos con la herramiente quicktype.io
const data = await response.json() as GitHubAPIResponse
```

### Interfaces
```ts
// Define el contrato de un objeto para especificar sus propiedades y metodos
interface Heroe {
	id: string
	name: string
	age: 30
	saludar: () => void
}

//-----------------

interface Producto {
	id: number
	nombre: string
	precio: number
	quantity: number
}

interface Zapatilla extends Producto {
	talla: number
}

interface CarritoDeCompras {
	totalPrice: number
	productos: Producto[]
}

// funciones en interfaces (dos métodos)
interface CarritoOps {
	add: (product: Producto) => void
	remove: (id: number) => void
}

interface CarritoOps {
	clear(): void
}

// las interfaces se pueden crear dos veces y se combinan en una sola interface
// los types NO tienen este comportamiento, devolvería error
```

### Interfaces vs Types
| Interfaces                             | Types                                         |
| -------------------------------------- | --------------------------------------------- |
| Siempre tienenq que ser objetos        | Pueden ser tuplas o formatos de string        |
| Se anidan cuando se vuelven a declarar | No se anidan, da error. Tienen que ser únicos |
| No tienen type indexing                | Tienen type indexing                          |
|                                        |                                               |

### Narrowing
```ts
function mostrarLongitud(objecto: number | string) {
	//como number no tiene length, checkeamos con javascript que devuelva el ...
	//... dato correcto
	if (typeof objeto === 'string) {
		return object.length
	}
}
```

### Type Guard
```ts
function checkIsSonic(personaje: Personaje): personaje is Sonic {
	return (personaje as Sonic).correr !== undefined
}

function jugar(personaje: Personaje) {
	if (checkIsSonic(personaje)) {
		personaje.correr
	}
}
```

### Instance of a class
```ts

```