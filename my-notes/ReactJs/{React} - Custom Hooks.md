Un custom hook en React es una función que permite encapsular lógica reutilizable y estado en componentes funcionales.

El funcionamiento de un custom hook es similar al de cualquier otra función de React. Puede utilizar los hooks existentes de React, como `useState`, `useEffect`, `useContext`, entre otros, para gestionar el estado y los efectos dentro del hook personalizado.

1. Lógica compartida: Si tienes lógica común que se repite en varios componentes, puedes extraerla en un custom hook para reutilizarla fácilmente en diferentes partes de tu aplicación.
    
2. Abstracción de API: Si necesitas interactuar con una API o realizar llamadas a servicios, puedes crear un custom hook que se encargue de manejar la lógica relacionada con las solicitudes y respuestas, abstrayendo los detalles específicos de la API.
    
3. Gestión de formularios: Los custom hooks pueden ayudar a encapsular la lógica de validación y manejo de formularios en un solo lugar, lo que facilita la reutilización en diferentes formularios de tu aplicación.
    
4. Manipulación del documento o eventos globales: Si necesitas realizar operaciones específicas en el documento o manipular eventos globales, puedes crear un custom hook para encapsular esa lógica y utilizarla en varios componentes.
    
5. Persistencia del estado: Los custom hooks también se pueden utilizar para gestionar el almacenamiento persistente del estado, ya sea en el almacenamiento local del navegador o en una base de datos externa.

```js
// useColor.js
import { useState } from "react";

const useColor = () => {
const [current, setCurrent] = useState(0);

const changeColor = () => {
	if (current === 2) {
		setCurrent(0);
	} else {
		setCurrent(current + 1);
	}
};
  
switch (current) {
	case 0:
	return [{ color: "red" }, changeColor];
	  
	case 1:
	return [{ color: "blue" }, changeColor];
	  
	case 2:
	return [{ color: "green" }, changeColor];
	  
	default:
	return [{ color: "red" }, changeColor];
	}
};
  
export default useColor;
```

```js
//App.js
import useColor from "./hooks/useColor";

export default const App = () => {
	const [color, changeColor] = useColor();
	  
	return (
		<div>
			<p style={color}>Texto ejemplo</p>
			<button onClick={changeColor}>Change</button>
		</div>
	);
};
  
```