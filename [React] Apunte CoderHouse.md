---
tags: [Coderhouse, React]
title: '[React] Apunte CoderHouse'
created: '2022-05-16T21:29:13.984Z'
modified: '2022-09-24T17:15:55.126Z'
---

# [React] Apunte CoderHouse

## CLASE 1

JAVASCRIPT : variables + tipos de datos + operadores + flujos de ejecución 
API web : https://developer.mozilla.org/en-US/docs/Web/API

var - let - const
operador REST/SPREAD (...)
destructuring (separar un array/objeto en variables individuales)

```js
Array.forEach()
Array.map()
Array.filter()
Array.reduce()
Array.sort()
```

## CLASE 2

### INICIANDO REACT APP

Para usar React usar
Bundler: programa empaquetador - junta muchos archivos en un archivo final (webpack)
webpack.js.org
Transpilador: transforma código (BABEL)

create-react-app : Crea una aplicacion react con una estructura de directorios estandar. Se ejecuta en la consola.

NODEJS: entorno de ejecucion de JavaScript como v8 el de google chrome, no tiene dom ni ajax. Es un servidor.

NPM: node package manager

1) instalar node
2) usar npm para instalar las create-react-app
3) Usar create-react-app para crear una aplicacion react

npm install -g create-react-app

create-react-app react-app-name
cd react-app-name

## CLASE 3

1) Borrar todo lo de la carpeta source (src)
2) Crear el módulo index.js, todo lo que este aca adentro tiene que pasar una sola vez al principio de la aplicacion y nunca mas. Está encargado de dibujar por primera vez lo que está en la aplicacion.
3) Cuatro lineas que siempre deben estar:
- Tener la variable React en scope
- Tener la variable ReactDOM en scope
- Tener un componente
- Tener una función render corriendo

### Import

Busca las variables dentro de alguna carpeta dentro de algun index.js.

```js
// manera vieja: CommonJS
	var x = require('x')

//manera nueva: ES6
	import x from 'x'
//trae la variable sin crearla en tu archivo actual.

//para importar primero hay que exportar

export default {}
export const x = {}
```
Traer la variable React en scope:
	import React from "react" ;

Tener la variable ReactDOM en scope:
	import ReactDOM from "react-dom" ;

Tener una funcion render corriendo: Le pasas dos parametros, la aplicacion de react previamente construida y en segundo lugar un nodo del DOM. Se recomienda no levantar la aplicacion en el body, las apps de react vienen con un div vacío:

ReactDOM.render(App() , document.querySelector("#ejemplo"));
ReactDOM.render(App() , document.getElementById("ejemplo"));

En el parámetro "a" tiene que haber un elemento de react. De tipo nodo o de tipo componente:

elemento react (nodo):
const a = <p>Hola Mundo</p>;
(esta "p" no es una etiqueta html)
Es un objeto de js que adentro tiene propiedades que describen la etiqueta, atributos, texto etc.
se llama sintaxis JSX (javascript y xml)


elemento react (componente):
 

VIRTUAL DOM : objeto muy grande que adentro tiene en forma de arbol invertido todos los elementos de la aplicación. Cada parte del dom se denomina fibra/nodo.
El nodo mas común es un elemento de React de tipo componente, es una partecita de html con lógica agregada.

En React no se modifica el DOM si no que se modifica el VIRTUAL DOM de React.

REACT: 
	
	1)Todos los componentes de React son funciones
	2)Todos los componentes de React tienen un retorno
	3)Todos los componentes de React arrancan en mayúscula, si no el compilador piensa que es una etiqueta y no un componente 
	4) Todos los componente se ejecutan en formato JSX (<Componente/>)

	(la funcion de un componente es mostrar algo en pantalla)
		
		function Componente(){
			return (x)
		}

		Componente() = <Componente /> = <Componente><Componente/>

		Si le quiero pasar prop entonces..

		<Componente nombre="Nicolás" />
		
		const Componente = () => {
			return (x)
		}
		
		class Componente{

		}

Componente que contiene toda la aplicación, es un componente general. App.js

No hace falta que el archivo tenga el mismo nombre que el componente, pero mejora la lectura que lo tengan.

const App = () => {
	return "Soy App"
}

export default App

Importo el componente en index.js:

import App from "./App"

importo los estilos en index.js:

import "./estulos.css"

Creando un componente:

const App = () => {
	return
	<>
		<header>
			<nav>
				<ul></ul>
				<ul></ul>
				<ul></ul>
			</nav>
		<header/>
		<main>
			<h1></h1>
		</main>
	</>
}

const NavBar = () => {
	return
		<nav>
		</nav>
}

export default NavBar


## CLASE 4

### COMPONENTES 1

Ponerle un id a una etiqueta en JSX:
	id=""

Ponerle una clase a una etiqueta en JSX:
	className=""

Ponerle un evento a una etiqueta en JSX:
	onClick=""

---------------------------------------

const App = () => {
	return
	<>
		<NavBar nombre="Horacio" />
	</>
}

Pasarle parámetros al componente.
Los parámetros se llaman "props"

const NavBar = (props) => {

	return (
		<header  id="main-header">
			<h1>Bienvenido {props.nombre}</h1>
				<nav>

				</nav>
		</header>
	);
}

export default NavBar

(Para meter una variable en JSX se mete entre llaves)

const App = () => {
	return
	<>
		<header>
			<NavBar nombre="Nicolás apellido="Florentin" />
		<header/>
		<main>
			<h1></h1>
		</main>
	</>

--------------------------------------

DESTRUCTURING :

const array = [1,2,3]

const [uno,dos,tres] = array

las asignaciones se mapean por posición, entonces queda:
uno = 1
dos = 2
tres = 3

Para objeto seria :

const objeto = {x:1 ,
				y:2, 
				z:3}

const {x:uno, y:dos, z:tres} = objeto

const uno = obj.x
const dos = obj.y
const tres = obj.z

PROPERTY SHORTHAND :

cuando tengo un objeto y adentro tengo que crear una propiedad y esa propiedad vale una variable con su mismo nombre

const nombre = "nicolas"

const persona = {
	nombre: nombre
}

const persona = {nombre}

------------------------------------------

const NavBar = (props) => {

	const {nombre, apellido} = props

	return
	<header  id="main-header">
		<h1>Bienvenido {nombre} {apellido}</h1>
			<nav>

			</nav>
	</header>
}

export default NavBar;

Los props son de solo lectura, se pueden modificar pero no tiene ninguna funcionalidad cambiarle el valor a las variables.

Los props pueden ser funciones

Los props siempre se mandan desde el lugar donde se llama al componente.

Otra forma de nombrar los props en el componente:

	const NavBar = ( {nombre,apellido} ) => {}


Otra forma de pasar props NO TAN COMÚN: luego llega al componente en el objeto con la key "children"

	<NavBar nombre="Nicolás apellido="Florentin">

	todo lo que este acá adentro se pasa como prop

	<NavBar />

--------------------------------------

CONSOLA DE REACT EN CHROME :

Instalar consola de React para ver que me traen los props sin usar console.log

"React Developer Tools" extension de Chrome

--------------------------------------

Cuando se re-renderiza un componente?

Cuando recibe un nuevo props o cambia el estado del componente.

Los props se pasan siempre de padre a hijo, nunca a los padres o componentes hermanos.

## CLASE 5

### COMPONENTES 2 : 

https://reactjs.org/docs/react-component.html

Todos los componentes tienen la capacidad de mandar o recibir props.

- State: 

	- Capacidad que tiene un compoente de guardar data y a medida que se

- Ciclo de vida: 

	Mount:
		- constructor : metodo que se ejecuta inmediatamente
		- render : se ejecuta al momento del dibujo
		- componentDidMount : despues de que se renderiza


	Update:
		- render : cuando se renderiza
		- shouldComponentUpdate : justo antes que te lleguen nuevos props.

	Unmount:
		- componentWillUnmount: el componente esta a un segundo de salir de pantalla


- Hoooks : 

	- Son funciones que se importan, ya vienen con la instalacion de React. Son preexistentes.
	- Pueden ser creados por el usuario
	- Los hooks no pueden estar en situaciones condicionales o bucles

 	- Closure de JavaScript : (?) 

 	- Son funciones que le dan funcionalidad extra a a un componente. Hay que importarlos

 	- useState
 	- useEffect
 	- useContext
 	- useReducer
 	- useLayoutEffect
 	- useRef
 	- useImperativeHandle
 	- useMemo
 	- useCallback
 	- useDebugValue

 	https://es.reactjs.org/docs/hooks-reference.html

Eventos en JS y jQuery:

- document.addEventListener("click",()=>{

})

- document.onclick = () => {}

- $(document).click( () => {} )

- Si quiero hacer un evento en React:

////////////////////////////////////////

import {useState} from "react"
import NavBar from "./NavBar"

const App = () => {

	const resultado = useState(0)
	const estado = resultado[0]
	const cambiareEstado = resultado[1]

	ó

	const [contador,setContador] = useState(0)

	const cambiarContador = () => {

		setContador(contador + 1)
	}

	return (
		<>
			<NavBar />
			<p>El contador va : {contador}</p>

			<button onClick = {cambiarContador} >click</button>
		</>
	)

- los eventos se escriben con camelCase
- importar el useState
- cuando cambia la variable se renderiza, ejecuta o remonta nuevamente el componente (nuevo ciclo de vida)
- "contador , setContador" [CONVENCIÓN] Tienen que relacionarse

Tipos de import : 
	
	- import con llaves : estas trayendo cosas de un export "a = 1" por ejemplo. Los exports NO default se pueden ejecutar n cantidad de veces.
	- import sin llaves : estas trayendo el export default. El default pasa una sola vez.



export default App

////////////////////////////////////////

- Escribir los eventos en camelCase!

- React reacciona a los cambios de estado, para eso sirven los cambios de estado

useState : 
	- NO es obligatorio que lleve parámetro
	- El parámetro es el valor del estado inicial con el que uno quiere arrancar
	- useState tiene retorno, tiene resultado. Lo podés meter adentro de una variable
	- retorna un array con dos elementos [estado inicial , función anónima]
	- la funcion que retorna es la funcion que hay que ejecutar para cambiar el valor inicial


## CLASE 6

# PROMISES, ASINCRONIA Y MAP

https://www.youtube.com/watch?v=ygA5U7Wgsg8

El componente se renderiza y arranca un ciclo de vida, es la ejecucion completa de un componente.
Cada componente se va a renderizar una y otra vez:

	- Si el componente cambia de estado
	- Si el valor de los props cambian

useEffect() :
	
	- Se ejecuta despues de que el componente se renderiza y cada vez que se vuelve a renderizar
	- import {useEffect}
	- Es un hook
	- No tiene retorno
	- Recibe 2 parámetros (a , b) = (función , array)
	- El array se denomina "array de dependencias", "parámetro de control" : Determina cuantas veces el efecto se va a termiar ejecutando. Una vez, mínimo, se ejecuta
	- Si el array esta vacío, la dependencia no existe
	- El efecto se ejecuta cada vez que las VARIABLES que ponga dentro del array cambien
	- Ejemplo de aplicacion :
		- Hacer pedidos a bases de datos
		- Si el cliente cambia de categoria de productos hacer el llamado
	- Cualquier cosa que no quiera dibujar, podria estar dentro de useEffect()
	- Para manejar ejecuciones asíncronas
	- Se escribe dentro de la lógica del componente
	- Clean Up (return) : 
		- retornando una funcion dentro del efecto, es funcion se ejecuta justo antes de que se destruya el componente.

PROMISES : 

	- La capacidad que tiene javascript de ejecutar código sin que eso te bloquee cosas.
	- Hay dos tipos de código:
		- sincrónico(bloqueante)
		- asincrónico(no bloqueante)
	- lo asincrónico siempre se ejecuta al final, despues de que se ejecute todo el código bloqueante

heap :
	- lugar fisico donde se alamacenan las variables. Se guardan en HEAP

stack : 
	- lugar fisico donde se ejecutan las funciones

queue:
	-	cola de las funciones esperando entrar al stack

web apis:
	- donde de ejecutan las funciones asíncronas, tambien vienen del stack. Cuando se termine se mueve de nuevo al queue en una cola de espera, y vuelve al stack ya finalizada.

Tres categorías de asincronia : 

	- Trigger : 
		- eventos como "onClick"
	- Timer :
		-tiempo fijo de delay en la ejecución. Ej: [ setTimeout() , setInterval() ]
	- Request : 
		-[callback | promise | async/await | funciones generadoras(generator)] 
		- no dependen de un evento ni de un tiempo específico (pedidos a base de datos, leer algun archivo local del usuario)

Los tres intentan abarcar el mismo problema : Cómo JavaScript te avisa que algo terminó?

Simular asincronía :

	- setTimeout (bloque, milisegundos) : Ejecuta el bloque de código luego de x milisegundos.

El cambio de estado, setFuncion() es asíncrónico, si pongo un console.log() abajo no se va a apreciar el valor actualizado.

Los console.log() siempre mejor ejecutarlos en el useEffect ya que se ejecutan al final de la lectura del código.


https://www.youtube.com/watch?v=8aGhZQkoFbQ
https://www.youtube.com/watch?v=cCOL7MC4Pl0&t=758s
https://www.youtube.com/watch?v=ygA5U7Wgsg8


PROMISE

const promesa = new Promise((a,b) => {
	
	//aqui va la operacion asincrónica

})

- Son objetos que representan la finalidad de una operacion asíncrona : 
	- Ejecuto un funcion asíncrona
	- Avisa que terminó
	- Te devuelve un objeto

Estados de una promesa  : 
	- pending (el codigo esta en proceso)
	- fulfilled (el código termino y NO dio error)
	- rejected	(el código termino y dio error)

Then :
	- promesa.then( ()=>{} ) :
	se ejecuta cuando termina bien la promesa

Catch :
	- promensa.catch( ()=>{} ) :
	se ejecuta cuando termina mal la promesa

Finally :
	- promesa.finally( ()=>{} ) :
	se ejecuta siempre

- Estados : pending | fullfilled | rejected

- otra sintaxis : 
	promesa
		.then( ()=>{} )
		.catch( ()=>{} )
		.finally( ()=>{} )

Parámetros de la promesa : 

	- Primer parametro de la promesa : Función. Si la ejecuto, el estado pasa a fullfilled

	- Segundo parámetro : Función. Si la ejecuto, el estado pasa a rejected.

Cuando se ejecuta la función a(RESULTADO) dentro de la promesa, el motor de la promesa cambia a FULFILLED 

Cuando se ejecuta la función b(RESULTADO) dentro de la promesa, el motor de la promesa cambia a REJECTED

El RESULTADO que termine dando la promesa, cae en el argumento de la funcion anónima del then o catch. Ej:

promesa.then(( RESULTADO )=>{});

let miPromesa = new Promise(function(resolve, reject) {
// "Codigo asíncrono"

  resolve(); // when successful
  reject();  // when error
});

// "Consuming Code" (Must wait for a fulfilled Promise)
miPromesa.then(
  function(value) { /* code if successful */ },
  function(error) { /* code if some error */ }
);

EJERCICIO 

const promesa = new Promise((a,b)=>{
	
	setTimeout(()=>{
		console.log("Pedido finalizado") ;
		a() ;
	},3000)

}) ;

Hacer un componente con un useEffect con una promesa que tarde 3 segundos


## CLASE 8

# ROUTING Y NAVEGACIÓN

Proyecto hasta el momento : 
	
		  ---- NavBar ---- Widget
		/
APP - ---- ILC ---- IL ---- ITEM
		\
		  ---- IDC ---- ID

Enrutamiento (Routing): [REACT ROUTER]
  
	- Como puedo ver una cosa u otra dependiendo de la situacion
	- Se usa para no cargar html css varias veces
	- Aplicar SPA (single page aplication)
	- Libreria que haga enrutamiento en React : REACT ROUTER
	- Enrutamiento React en general, no sólo para web

Instalar React Router : 

	1- npm i react-router-dom
	2- Identificar enrutador : 

		- En algún componente del árbol tiene que estar incluido un componente enrutador
		- No hace falta que toda la aplicación este dentro de un enrutador
		- Si App, por ejemplo, está incluida en un enrutador, todos los hijos estan incluidos

	3- Enrutadores : 

		- BrowserRouter : History API (es la que usamos en este proyecto)
		- HashRouter : location.hash
		- MemoryRouter : Rutas de memoria
		- StaticRouter : SSR (server side rendering al contrario de client side rendering CSR)

	- Solo hay que importar el componente y ya funciona
	- La dificultad yace en saber que hace cada componente

	4- Poner todo el componente App en un BrowserRouter

		- A partir de App para abajo les puedo poner cualquier componente de la librería
		- import {BrowserRouter} from 'react-router-dom'

		<BrowserRouter>
		
			<Componente1 />
			<Componente2 />
			<Componente3 />

		<BrowserRouter />

	5- Componentes más importantes : 

		- Link o NavLink :

			- Genera en el DOM una etiqueta <a> con la redirección URL
			- Generan links en pantalla, navlink tiene un poco más de css, en vez de hacer una etiqueta <a>. Se reemplaza por el componente. import {Link} from 'react-router-dom' <Link to="/categoría1"> link </Link>
			- El beneficio del componente es que la página NO recarga, si no que CAMBIA LA URL pero no se recarga la página completa
 			- Tambien puede ser "/categoria/1"

 		- Route : 

 			- <Route />
 			- Te permite mostrar algo en pantalla si coincide con la URL en donde estas parado
 			- Es como un identificador de las rutas de <Link>, link cambia la URL y route la lee e interpreta mostrando los componentes incorporados
 			- Necesita dos props : path="" y component=""
 			- path : Se pone la URL que se busca coincidir (ej: "/categoria/:id") los dos puntos indica que espera algo, un ID en este caso. Es un prop dinámico.
 			- component : Qué componente se quiere mostrar en caso de coincidencia (ej: component={ItemListContainer})
 			- En component va sin comillas, le pasas la variable importada escapando de JSX

 			- Ejemplo en el proyecto :
	 			- <Route path="/" component="{ItemListContainer}" />
	 			- <Route path="/categoria/:id" component={ItemListContainer} />
	 			- <Route path="/item/:id" component={ItemDetailContainer} />

	 	- Switch : 

	 		- Hace que se muestre un solo componente, nunca dos en simultáneo
	 		- Ejemplo : 

	 			<Switch>
		 			<Route path="/" component="{ItemListContainer}" exact />
		 			<Route path="/categoria/:id" component="{ItemListContainer}" exact />
		 			<Route path="/item/:id" component="{ItemDetailContainer}" exact />
		 		<Switch />
			- el EXACT sirve para que solo se muestre si es exactamente ese path

Con la instalacion de la librería se instalan TRES HOOKS NUEVOS : 

	- useHistory
	- useLocation
	- useParams :
		- sirve para traer las partes dinámicas de la URL que coincidieron con el path
		- se ejecuta llamando a la funcion y retorna un objeto con el path dinámico que recibe. ej: "/:id"
		- la propiedad del objeto que retorna en este caso seria "id" y su valor, el valor dinámico. En este caso 1 o 2


## CLASE 9

# EVENTOS

Tipos de eventos : 
	-	Eventos automáticos : En determinado tiempo la aplicacion hace algo.
	- Eventos manuales : Son todas las interacciones del usuario que tienen algun típo de respuesta o evento
	- Ejemplo : <button onClick={input}> BUTTON </button>
	- Invocar el removeEventListener en la funcion de limpieza de nuestros Hooks en donde los hayamos registrado

Synthetic events : 
 - Normaliza y estandariza eventos
 - Siempre que se registre un evento vía React/JSX con onClick, no obtengo el evento nativo, si no uno sintético
 - Se destruyen al terminar la ejecucion de la funcion vinculada (importante)
 - Puedo acceder al evento nativo via evt.nativeEvent

e.stopPropagation() : 
	- Evita que el evento suba a componentes padres 

e.preventDefault() :
	- Cancela el evento si este es cancelable, sin detener el resto del funcionamiento del evento, es decir, puede ser llamado de nuevo}
	- Cancela el comportamiendo por default del evento


Orientacion a eventos : 
	- Permite mover la lógica compleja a componentes de menor orden.
	- Si ambos se comportan igual, el parent no lo sabrá aunque sus implementaciones sean distintas.
	- Permite que el parent se encargue del resultado final sin darle esa responsabilidad a sus children.


## CLASE 10

# CONTEXT API

Funcionalidad : 
	- Permite pasar una variable única cross-app
	-	Evitar pasar props de componente a componente y llamarlos directamente en el componente que se necesita
	- Es una api que ya viene con react
	- Siempre que se pueda usar props react lo prefiere, dejar context para casos especiales

En el componente origen : 
	- Hay que importar el objeto contexto {createContext}
	- Un contexto createContext(), retorna un objeto con dos componentes adentro {Consumer,Provider} = createContext({object}) (no es necesario hacer destructuring)
	- export contexto = createContext({object}) (necesario)
	- Se crea en el componente origen donde está el prop

En el componente destino : 
	- Se llama al hook {useContext}
	- import contexto from './location'
	- const resultado = useContext(contexto)
	- console.log(resultado) ---> object
	- La data del contexto es de solo lectura, no se puede modificar

Patrón PROVIDER : 
	-	Ejemplos :
		-	Quiero modificar el contexto y sincronizar cambios
		-	Agregar o borrar elementos al carrito
	-	Crear componente provider que va a ser el provider del contexto y me va a permitir modificar el contexto, ej : CustomProvider=()=>{}
	- Conceptualmente es como guardar data en una variable de scope global
	-	La aplicacion es muy grande y quiero independizar el componente para que no dependa de sus padres o hijos y que sea mas adaptable a nuevos cambios

Componente Provider : 
	-	En algun lado va a haber uno o varios estados
	-	Un estado sería el dato que se quiere globalizar :
		-	const [productos,setProductos] = useState([])
	- Provider me va a hacer de nexo entre el objeto contexto y los cambios de un componente
	-	En el componente estarán los métodos que me permitan modificar el contexto o fijarme si están duplicados :

	import {createContext,useState} from 'react'

		export const contexto = createContext()

		const {Provider} = contexto

		const CustomProvider=({children})=>{

			const [productos,setProductos]=useState([])
			const addProduct=(id)=>{}
			const removeProduct=(id)=>{}

			return(
				<Provider value={{productos,addProduct,removeProduct}}>
					{children}
				</ Provider>
			)
		}
	
	- En el retorno del componente : 
		-	quiero independizar el provider del componente hijo (hijo dinámico)
		return(<></>)

		- Poniendo el {children} dentro del Provider te aseguras de que el children del componente sea dinámico y que reciban el contexto independientemente de la ubicación

- En el momento en que el provider está presente, el objeto contexto es como que deja de existir.
-	El Provider pasa a ser el contexto
- Envolver los componentes con <CustomProvider></ CustomProvider> para que todos los hijos reciban el contexto

- RESUMEN : A partir del <CustomProvider> hacia abajo, todos los componentes pueden llegar al contexto que esta determinado por el value. Como el value es el estado de un componente y puede cambiar, si llega a cambiar el estado el componente se vuelve a rejecutar, se vuelve a repintar el return y el contexto cambia, y las cosas que usan el contexto cambian.


## CLASE 11

# TÉCNICAS DE RENDERING

Rendering condicional : 
	-	Con loading (true) y setLoading como estado : 
		-	return (
				loading ?
					<p>Cargando productos...</p>
					:
					<p>Productos cargados!</p>
		)

	- Otro ejemplo (return temprano) : 
		- export function TextComponent ({ user = true }) {
			if (!user) {
				return <h2>Usted no esta logueado</h2>
			}
			return <h2>Usted esta logueado puede ver la pagina y tiene datos sensibles</h2>
		}

	- Otro ejemplo (Inline con fragment) : 
		- export function TextComponent ({ condition = true }) {
			return (
				<>
					{condition && <h2>Usted no esta logueado</h2>}

					{!condition && <h2>Usted esta logueado puede ver la pagina y tiene datos sensibles</h2>}
				</>
			)
		}

	-	Otro ejemplo (Inline ternary, crea un solo nodo) :
		-	 export Componente = ({ condition = false }) {
		return (
			<>
				<h2>{ condition ? "uds esta logueado" : "ud no esta logueado" }</h2>
			</>
			)
		}

Evitar re-renderizado en componentes hijos si...
	-	El componente es puro
	-	Tenemos la certeza de que las mismas props producen el mismo render
	-	 Es muy caro renderizar listas largas y compleja

### MEMO :

Dependencia de React, Memo : 

		-	Dependencia de React
		-	Le pasamos dos argumentos (callbacks)
		-	Primer agumento es el componente
		-	const Componente = memo ( ()=>{} , arg2 )
		-	Si react no detecta cambios no vuelve a renderizar
		-	Al segundo argumento se le pasan dos parametros (oldProps, newProps)
		- Podes agregarle un callback que devuelva un booleano y decidir si renderizar de nuevo

```js
import { memo } from "react";

const Todos = ({ todos }) => {
  console.log("child render");
  return (
    <>
      <h2>My Todos</h2>
      {todos.map((todo, index) => {
        return <p key={index}>{todo}</p>;
      })}
    </>
  );
};

export default memo(Todos);
```


## CLASE 12 

# FIREBASE

Dos tipos de bases de datos : 

	-	RELACIONAL (SQL)
	- NO RELACIONAL (NoSQL) [firebase]

Usar Firesabase como base de datos, nos va a dar funciones y metodos que ejecutamos y nos hace la base de datos.

Firebase me da un servicio de nu

-	ir a la consola

La organizacion de los datos se da por colecciones
La coleccion puede o no existir para llamarla 
Los datos se deben almacenar de a uno
Almacenar al menos uno de cada categoría

Integracion con la aplicacion : 

	-	Seguir los pasos de la documentacion : 

import firebase from "firebase/app";
import "firebase/firestore"
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "AIzaSyA1PpW2f3nSgYQIJVKo75rO7WTgXMCG_Fg",
  authDomain: "react-ecommerce-86e72.firebaseapp.com",
  projectId: "react-ecommerce-86e72",
  storageBucket: "react-ecommerce-86e72.appspot.com",
  messagingSenderId: "78590878183",
  appId: "1:78590878183:web:eac80eee54bcbec2911d42"
};

// Initialize Firebase
const app = firebase.initializeApp(firebaseConfig);

export const firestore = firebase.firestore(app)

## CLASE 13

### FIREBASE II

-	En el detalle del producto usar el metodo "doc()" para filtrar la colleccion y devolver un solo producto
-	Para filtrar por categorias usar el metodo "where()" sobre la coleccion para devolver los productos por categoria (NO TRAER TODOS LOS PRODUCTOS Y FILTRAR EN EL FRONT)

get trae todo

doc trae uno, le metes un string en el argumento

where filtra

	-	No quiero guardar los datos de confirmacion dentro de la coleccion de productos
	-	Guardar la confirmacion en otra coleccion
	-	No hace falta crearla desde la página
	-	Lo que se agrega a la collecion siempre tiene que ser objeto
	
	-	Crear colección : 
		-	Ejemplo : 
			const db = firestore
			const newCollection = firestore.collection("ordenes")

			const orden =
			{
				products : carrito
				user : usuario
			}
			
			const query = newCollection.add(orden)

Hacer un estado con onchange para cada uno de los campos, nombre telefono email



## Cómo CREAR un contexto : 

import React, { createContext } from 'react'

const UserContext = createContext()

const UserProvider = ({ children }) => {

	const data = {
		key1: value1,
		key2: value2
	}

	return (
		<UserContext.Provider value={data}>
			{ children }
		</UserContext.Provider>
	)
} 

export { UserProvider }
export default UserContext


## Cómo CONSUMIR un contexto : 

import React , { useContext } from 'react'
import UserContext from 'context/UserProvider.jsx'

const componenteConsumidor = () => {

	const data = useContext(userContext)
	
}

