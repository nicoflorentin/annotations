- por qué react ? 
- enrutamiento
	- react router dom
	- guard
	- enrutameinto a nivel hijos
	- obtener datos de la url queryParams
- manejo de estado
	- context
		- global state
		- por pagina
		- useReducer
	- redux
		- redux toolkit
		- redux query
	- swr (state while revalidate)
	- zustand
	- jotai
- diff entre ReactNode y JSX.Element
- useMemo vs useCallback vs useRef
- deteccion de cambios
	- cuando hay un cambio
	- como impacta el modo estricto
	- cosas que se pueden hacer para controlar un render no deseado
	- parámetros
	- cambio
		- montaje
		- cambio de estado
		- cambio de parámetros
	- commit
- mejores formas de compartir informacion entre componentes
	- padre a hijo
		- drop drilling
		- composition patterns
	- hermanos
		- observables - servicio
	- porque usar si es posible el composition pattern en vez de un componente
- batching de estados
	- cada una de las cosas que haciamos dentro de un metodo se van agrupando
	- set((state) => {logica al state})
- el nuevo compilador de react 19
- que cosas cambian con react 19
-  useState
- useEffect
	- cuando utilizarlo correctamente
	- que va dentro del arreglo de dependencias
	- que pasa si quiero ejecutar un metodo async dentro del mismo
- react hook form
	- useForm
	- validaciones con schema
		- zod
		- yup
- modelar con typescript
- arquitectura que se utiliza
	- scream arquitecture
	- clean architecture
	- container / presentational architecture
- axios
	- interrupt
	- api
	- interceptors
- portals
- high order components
- custom hooks
	- cuando utilizar
	- que conlleva
- suspense y lazy
	- que significa
- tipos de styling
	- module css / scss
	- variable style
	- objeto en el inline style
- errorBoundary
- manejo de cache

**PORQUE REACT**
es una biblioteca, libreria ultraflexible que nos posibilita el desarrollo eficiente y rapido con poca curva de aprendizaje para proyectos cortos estaticos o muy dinamicos y nos va a esrvir para proyectos de requerimientos muy dinamicos y mucho prototipado
esa flexibilidad le da peligro, hay que utilizarlo bajo el cuidado de un experto

**ENRUTAMIENTO**
react router dom, nos predispone un conjunto de metodos que nos da tanto la navegacion como la guardia de rutas a traves de logicas internas
enrutamiento a traves de hijos

**MANEJOS DE ESTADO**
context : viene dentro de react., nos permite un control individual de una pagina como tambien a un nivel global de toda la aplicacion
necesita un provider, engloba a que luygar dentro de la aplicacion va a a afectar.
utilizar con logica que se utilice poro, la rerenderizacion de context es costosa
recomendado utilizarlo por pagina, por feature que se vea en pantalla.
si hay demasiada logica y es un estado enorme (ej un contexto de toda la aplicacion) utilizar **usereducer** que utiliza single source of truth architecture en el cual dentro del mismo tenemos info certera eficiente y al dia de lo que sucede nuestra aplicacion. action con payloads

**REDUX**
biblioteca. cuando hay que tener mucho mas control sobre los datos. va mas alla de context.
tenemos redux toolkit, utiliza tambien action y payload

**STALE WHILE REVALIDATE**
guarda la informacion en pantalla, la cachea, si se valida que la informacion traida del back es distinta, se rerenderiza, caso contrario no se rerenderiza, compara las respuestas de la api.

**ZUSTAND**
biblioteca de manejo de estados simplificada. es mas liviano que redux. tiene menos boilerplate code.

**JOTAI**
es distinto a los otros state management, es un useState a nivel global
esto se llama "atomo"

**REACT NODE Y JSX ELEMENT**
jsx element es un html con logica, react node hace representacion a todo aquello que react puede renderizar

**USEMEMO**
guarda en memoria el resultado de funciones muy costosas que ante un mismo parametro devuelve un mismo resultado
funcion declarativa. si el parámetro es muy dinamico y cambia demasiado es un problema porque almacenamos en memoria demasiados resultados ademas de ejecutar el metodo

**USECALLBACK**
utilizamos para guardar la referencia de una funcion
cuando hacemos un render dentro de un componente volvemos a instanciar tambien todos los metodos del mismo
guardamos la instnaica de un metodo para que no se vuelva a crear
se hace por un arreglo de dependencias
se usa para que el componente hijo al cual le pasamos la referencia no lo detecte como un cambio y rerenderice cuando no es necesario

**USEREF**
guardar valores internos que se utilicen dentro de las operaciones pero a la hora de cambiarlos no rerenderiza.
tambien se pueden referenciar elementos del dom y podemos interactuar con ellos desde la mismo logica.

**DETECCION DE CAMBIOS**
el modo estricto es un tag que se pone en mainjs y engloba a app component
hace que lo que esta adentro se renderice 2 veces, se monta, carga el estado, se destruye, se vuelve a cargar, se vuelve a tratar de recuperar dicho estado y lo comrprueba.
es una validacion extra en el entorno de desarrollo, cuando vas a produccion esto no se ejecuta.

**CONTROLAR RERENDER NO DESEADO**
contorlar parametros, referencias, useeffect acordes, no usarlos para una logica de cambio de estado. solo usarlo para sincronizaciones con cosas exteriores.

**COMMIT**
es la comparacion entre el dom y el dom virtual

**MEJORES FORMAS DE COMPARTIR INFO E COMPONENTES**
prop drilling, hijo a hijo a hijo a hijo, no es escalable y no se pueden reutilizar los componentes
composition pattern : cada componente tiene su lógica particular, por separado y se puedan expandir. la logica queda solo dentro del padre, el hijo nunca se entera de la logica que lo contiene.
componentes hermanos : podemos utilizar observables a traves de un servicio, creamos un servicio, el servicio hace un singleton, el singleton se comparte en toda la aplicacion y dentro se comparte la variable y se comparte.
si puede ser, utilizar **rxjs** y behaviour subject (sujeto bidireccional y guarda el estado del ultimo evento que se emita)
context tambien puede manejar varaibles entre hermanos

**BATCHING DE ESTADOS**
si tenemos un useffect y tenemos 5 setstate dentro del mismo, no se hacen los cambios hasta que se termine de usar esta logica.
es recomendable ejecutar un metodo que tome el valor del estado al momento de ejecutar ese metodo

**NUEVO COMPILADOR DE REACT 19**
**QUE COSAS CAMBIAN EN REACT 19**
se va el usememo, usecallback

**USESTATE**
crear un valor de estado dentro de un componente, persiste entre los rerenders

**USEFFECT** 
sincronizar las cosas con entidades externas (contexto, endpoint, observable, parametro).
nunca utilizarlo para reaccionar dentro de un estado de un mismo componente
dentro del arreglo de dependencias va todo aquello que pueda cambiar y sea utilizado dentro del mismo.

**LA MEJOR FORMA DE EJECUTAR UN METODO ASYNC CON USEFFECT**
crear el metodo dentro del useffect y ejecutarlo dentro del mismo (recomendad)
ponerlo afuera pero hay que inicializarla fuera del componente porque si lo pongo adentro cada vez que hay un cambio se vueve a crear y vuelve a escribir todo el useeffect y se ejecuta de manera infinita.

**USEFORM**
manejo de formularios que posee un metodo useform que nos da desde el estado, la data, los errores, se puede asociar un tipo de validacion como **zod** o **yup**
nos permite una manera de registrar ante cada unos de los parametros de nuestro fromulario.
muy facil modelar componentes que se encarguen solo de los inputs

**MODELAR CON TYPESCRIPT**
carpeta models dentro de cada funcionalidad
no utilizar nunca any
saber la diferencia entre unknown y never y any
modelar con typescript significa no hacer un solo interface enorme con mas de un nivel
cuando utilizar un type y un interface
utilizar interface para todo hasta que necesitemos algo más (asi dice la documentacion)
el type brinda mas cosas como usar enums como keys

**ARQUITECTURAS**
scream : las cosas tienen que gritarte en la cara la lógica
clean : diferentes niveles, dominio, toda la logica, adapter para comunic entre app y parte externa
container : los container tienen la logica de como renderizar las cosas, logica de negocios
la app: son los componentes
los componentes reciben las peticiones de los endpoints y adaptarlos para no tener que luego mantenerlos

**AXIOS**
no siempre es necesaria, se puede hacer casi todo lo mismo con fetch
interrupt : se hace por medio de un contexto
interceptor : intercept peticiones y respuestas

**PORTALS**
capacidad de renderizar codigo o componente en cualquier lugar de la aplicacion, se usa mucho para modales.

**HIGH ORDER COMPONENTS**
es un componente que nos da la posibilidad de extender nuestro componente. la documentacion recomienda usar composition pattern

**CUSTOM HOOKS**
utilizar siempre y cuando tengamos logica repetida que depende de un estado.
adentro tambien tiene un useeffect
devolvemos los estados para afuera

**SUSPENSE Y LAZY**
lazy : renderizar componentes solo cuando se necesitan solamente dentro del suspense
suspense : renderiza un placeholder, algo opcional, hasta que lo que pedimos renderizar

**TIPOS DE STILYNG**
modulos de css, son isolated

**ERROR BOUNDARY**
se hace con clases, se controlar los distintos tipos de acciones que pasan en la aplicacion sobre todo las de error, y accionar sobre ellas.