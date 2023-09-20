- En este ejemplo se agrega una funcion de contador a un componente a través de una funcion HOC
- Se le pasa un valor por parámetro
- Tambien recibe una prop desde el componente padre

Componente contenedor : 
```jsx
// Hoc.jsx

import React from 'react'
import ClickCounter from './ClickCounter'
import HoverCounter from './HoverCounter'
  
const Hoc = () => {
  return (
    <div>
      <ClickCounter/>
      {/* este componente en realidad es NewComponent, retornado por la funcion withCounter */}
      <HoverCounter secret='password'/>
    </div>
  )
}
export default Hoc
```

Componente al que se le aplica la lógica del HOC : 
```jsx
///HoverCounter.jsx

import { useState } from "react"
import withCounter from "./withCounter"
  
function HoverCounter(props) {
  const { counter, incrementCounter } = props
  const [fontSize, setFontSize] = useState(10)
  
  return (
    <div>
      {/*This time, instead of listening to clicks,*/}
      {/*Listen to hover events instead*/}
      <button onMouseOver={() => setFontSize(size => size + 1)}>Increase on hover</button>
      <p style={{ fontSize }}>Size of font in onMouseOver function: {fontSize}</p>
      <p> Value of 'name' in HoverIncrease: {props.name}</p>
      <button onClick={() => incrementCounter()}>Increment counter</button>
      <p> Value of 'counter' in HoverIncrease: {counter}</p>
      <p>secret: {props.secret}</p>
    </div>
  )
}
 
export default withCounter(HoverCounter, 5)
```

Función que espera un componente como argumento para aplicarle la lógica : 
```jsx
// withCounter.jsx

import React, { useState } from "react"
  
//crea una funcion que recige un componente y un valor arbitrario
const updatedComponent = (OriginalComponent, customValue) => {
  //crea un componente nuevo, no importa el nombre
  const NewComponent = props => {
    // crea un estado propio del componente
    const [counter, setCounter] = useState(10)
    return (
      //renderiza el componete que recibe por parametro y le agrega las props del HOC y su logica
      <OriginalComponent
        counter={counter}
        incrementCounter={() => setCounter(counter => counter + customValue)}
        name="Nicolas"
        //en caso que el componente original reciba props del padre, hacer destructuring
        {...props}
      />
    )
  }
  //retornar el nuevo componente que es el original component mas las props otorgadas por el hoc y el componente padre
  return NewComponent
}
 //exporta la funcion que recibe por parametro el componente y el valor arbitrario y que retorna un componente nuevo con toda la logica y las props agregadas
export default updatedComponent
```