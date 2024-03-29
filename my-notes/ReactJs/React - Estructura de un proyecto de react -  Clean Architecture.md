Los componentes tienen la logica de negocios, accionan sobre las cosas que estan en el modelo como los datos de usuario etc

## Estructura de carpetas
- adapters **(reutilizable)**
- assets
- components **(reutilizable)** 
- contexts
- hooks **(reutilizable)**
- interceptors **(reutilizable)**
- models **(reutilizable)**
- pages
- redux
- services **(reutilizable)**
- styled-components **(reutilizable)**
- utilities

![[Pasted image 20231003122757.png]]

##### Services
Servicios externos lugares que llamamos para buscar informacion

##### Interceptor 
Adaptar lo que enviamos y lo que recibimos
##### Components
Lóiica de negocios

##### Hooks
Custom hooks

##### Reusable modules
adapters - components - hooks - interceptors - models - services - styled-components

![[Pasted image 20231003123352.png]]

#### Adapter example : 

```jsx
import { EndpointUser, User } from '@/models';

export const create AddaptedUser = (user: EndpointUser) => {
	const formatteduser: User {
		name: user.name,
		lastName: user.last:name
	}
	
return formattedUser
}

export default AddaptedUser
```
 
##### Assets
multimedia, tipografias

##### Components
Depende si se usan en toda la aplicacion o solo en una vista

##### Contexts
- Estados que solo se encuentran dentro de una vista o cosas que son muy simples
- Crear la carpeta context dentro de una carpeta page

##### Redux
- Carpeta que contiene el redux 
- Cosas que pueden estar en la aplicacion en todo momento

##### Custom Hooks
Código reutilizable que controla los ciclos de vida de un componente

##### Interceptor
Los interceptores de solicitudes HTTP te permiten interceptar y manipular estas solicitudes antes de que se envíen al servidor o después de que se reciban las respuestas. Esto es útil para agregar encabezados personalizados, manejar errores globalmente, realizar autenticación

##### Models
Concepto de typescript

##### Pages
Cada una de las vistas, con sus carpetas de componentes, contextos, etc

##### Services
Todas las llamadas y los servicios para comunicarnos con la API

##### Utilities
Lógica reutilizable como formatters o logica muy pequeña 