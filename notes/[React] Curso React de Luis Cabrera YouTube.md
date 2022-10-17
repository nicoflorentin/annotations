---
tags: [React]
title: '[React] Curso React de Luis Cabrera YouTube'
created: '2022-07-28T04:30:04.413Z'
modified: '2022-09-28T06:09:44.109Z'
---

# [React] Curso React de Luis Cabrera YouTube

Usar React Developer tools

NodeJs: entonrno de ejecucion de js
NPM: gestor de paquetes de Javascript, con esto instalamos React y Bootstrap por ejemplo

node -v : muestra la version de NodeJS
npm -v : lo mismo

## Editor de código : VSCode o SublimeText

### VSCode Extensions : 
- ES7 React/Redux/GraphQL/React-Native snippets
- Simple React Snippets
- Bracket Pair Colorizer
- Auto Rename Tag
- Prettier - Code Formatter

### Shorcuts : 

- (ctrl+|) : side by side edit
- (ctrl+s) : save
- (ctrl+h) : replace
- (ctrl+s) : find
- (ctrl+ñ) : open terminal

## Crear aplicacion React

En la consola...

1) - npx - create-react-app MyReactApp < nombre de la aplicacion
    - cd MyReactApp
    - npm start


## Estructura de la aplicación
- package.json : dependecias de la aplicación
  - start crea servidor de desarollo y ver app en tiempo real
  - build crea empaquetado comprimido para lanzarlo a produccion
  - test lanzar testings creados para la aplicacion
  - ejecto permite acceder a ciertas configuraciones
- readme : expresa info relevante del proyecto
- gitignore : ignorar archivos que no son necesarios en el repositorio

- index.html : esta la etiqueta con id root, el unico div del index. Contiene toda la aplicacion React.
Carga el componente App.js

2) Vaciar carpeta src y crear index.js

```js

import React from 'React'
import ReactDOM from 'react-dom'
import App from './App'

ReactDOM.render(
  <App/> , document.querySelector("#root")
)
```

En App.js : 

```js
import React from 'React'

const App = () => {
  return (
    <>
    <h1>Soy la App<h1>
    </>
  );
}

export default App ;

```

El primer parámetro es el componente a renderizar y el segundo parámetro es el id del div del index.js

- Cada componente solo puede retornar un solo div

- En src creamos carpeta components

## Instalar Bootstrap :

Pegar el link del CDN en el <head> del index.html

## Nota sobre funciones en el onClick

- Si la función del onclick esta declarada sin argumentos, ésta se ejecuta sólo con el evento
- Si la funcion del onclick esta declarada con argumentos, ésta se ejecuta cuando se renderiza el componente y luego sólo con el evento. En este caso para que se comporte como una llamada a funcion sin argumentos hay que ejecutarla desde una funcion anónima (flecha) 

Ejemplo:
```html
<button onClick={ () => todoDelete(id) } />
```

## Uso de Back-ticks : 

Back-Tics Syntax
Template Literals use back-ticks (``) rather than the quotes ("") to define a string:

Example
let text = `Hello World!`;

## Nota sobre array.map() :
- si el bloque del callback esta entre parentesis, automaticamente retorna lo que esté dentro
- si el bloque del callback esta entre llaves habrá que retornar manualmente

``` js
//se retorna automaticamente:
array.map( () => (/* bloque de código */) )

//se retorna manualmente:
array.map( () => { /*bloque de código*/ } )

//otra forma (cuando hay una sola sentencia en la función) :
array.map ( argum => condicional ? retorna1 : retorna2 )
```

## Operador Spread :

```js
const changedObject =
  {...object,
  prop: changedProp
  }

```

Tambien se le puede cambiar la ubicacion al spread : 

```js
const changedObject =
  {prop: changedProp,
  ...object  
  }

```


## Manejar el argumento del evento:

Cuando se dispara un evento el primer argumento que recibe la funcion es el objeto del evento: Aqui puede llegar el value del formulario :
- [event.target.name] : event.target.value : Aqui se usan corchetes para usar variables dentro de las propiedades de un objeto 
Se puede usar el método preventDefault para evitar que el submit del formulario recargue la página

```js
const formChange = (event) => {
  const changedFormValue = {
    ...formValue,
    [event.target.name] : event.target.value 
    // los corchetes indican propiedad con nombre de variable
  }
  setFormValue(changedFormValue)
}
```

```js
const handleSubmit = (e) => {
  // para evitar que al submitear no se recargue la pantalla
  e.preventDefault()
  todoAdd(formValue)
  setFormValue(initialFormValue)
```

Estado de error : 

Hacer un estado en el componente para el manejo de errores

```js
const [error, setError] = useState(false)
```

## Renderizado condicional con JSX

```js
{error ?
  ( <div className='alert alert-danger mt-2'>
  { error }
  </div>
  ) : (<p></p>)
}
```
otra forma : 
```js
{error && (
  <div className='alert alert-danger mt-2'>
  { error }
  </div>
)}
```

## Método trim para validad formularios (borrar espacios vacíos): 
```js
if (title.trim() === '') {
  setError('Título vacío')
  return ;
}
```
## Usar un timeout para manejar alertas temporales con un estado de error o succes :
```js
setTimeout( () => {
  setSuccessMessage(null)
},2000)
```

## NETLIFY para subir el proyecto a producción
https://www.netlify.com/

## Abrir el editor de codigo desde la consola
Situado en el directorio del proyecto usar "code ." para abrir el editor de código con el proyecto cargado (instalar, ni idea como)

## Hacer un fetch y utilizarlo en useEffect

useEffect no admite funcinoes asincronas por lo tanto el await hay que usarlo por fuera del useEffect

```js
const updateQuote = async () => {

		console.log('useEffect iniciado')
		const url = 'https://www.breakingbadapi.com/api/quote/random'
		const response = await fetch(url)
		const [ {quote: text , author} ] = await response.json()

		// antes de hacer destructuring
		// setQuote({
		// 	text : quote,
		// 	author : author
		// })

		setQuote({
			text,
			author
		})
	}

	useEffect(() => {
		updateQuote()
	}, [])
```

- Las llamadas a las apis deben hacerse en un archivo separado en la carpeta src/helpers

- Asignar lo que hay en la posicion 0 de un array a una variable: 

```js
///ejemplo: data
const [data] = await response.json()
```

### Acceder a datos del objeto de la opcion seleccionada de una etiqueta select

```html
<div>
  <select name="select"
          onChange={ (e) => { updateDog(e.target.value , e.target.options[e.target.selectedIndex].text) } }>            
    { breeds.map( (breed) => <option value={ breed.id } key={ breed.id } breed={ breed.name }>{ breed.name }</option>  ) }
  </select>
</div>
```
- e.target.value accede a los valores de los atributos de la etiqueta select, ***no*** accede a los valores de los atributos de las etiquetas option!

## Manejo de Errores

- En este caso, throw Error dentro de una funcion que retorna una promesa, puede ser utilizado con .catch()

```js
const getBreeds = async () => {
  const url = 'https://api.thedogapi.com/v1/breeds'
  const response = await fetch(url)
  const data = await response.json()

  if (!response.ok) {
    const {url, status, statusText} = response
    throw Error(`Error: ${status} ${statusText} in fetch: ${url} `)
  }

  return data
}
```

## Estructura de la aplicación

- /public : index.html y manifest.json
- /src :
  - /src/helpers : llamados a apis
  - /src/components : componentes y sus estilos


