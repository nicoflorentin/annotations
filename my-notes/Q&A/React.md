1. **Que son los componentes presentacionales?** 
Se centran en cómo se ven las cosas.
Pueden contener tanto componentes presentacionales como contenedores dentro, y usualmente tienen algo de marcado DOM y estilos propios.
A menudo permiten contenidos a través de `this.props.children`.
No tienen dependencias con el resto de la aplicación, como acciones o almacenes de Flux.
No especifican cómo se cargan o modifican los datos.
Reciben datos y callbacks exclusivamente a través de props.
Rara vez tienen su propio estado (cuando lo tienen, es un estado de la UI en lugar de datos).
Se escriben como componentes funcionales, a menos que necesiten estado, hooks de ciclo de vida o optimizaciones de rendimiento.
Ejemplos: Página, Barra lateral, Historia, Información del usuario, Lista.

2. **Que son los componentes contenedores?**
Se ocupan de cómo funcionan las cosas.
Pueden contener tanto componentes presentacionales como contenedores dentro, pero generalmente no tienen marcado DOM propio, excepto por algunos `div` de envoltura, y nunca tienen estilos.
Proveen datos y comportamiento a componentes presentacionales u otros componentes contenedores.
Llaman a acciones de Flux y las proporcionan como callbacks a los componentes presentacionales.
A menudo son stateful (con estado), ya que tienden a servir como fuentes de datos.
Generalmente se generan usando higher order components (HOC), como `connect()` de React Redux, `createContainer()` de Relay, o `Container.create()` de Flux Utils, en lugar de ser escritos manualmente.
Ejemplos: Página de usuario, Barra lateral de seguidores, Contenedor de historias, Lista de usuarios seguidos.

3. 