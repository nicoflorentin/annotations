### Curso Astro 5 Midu

puedo sacar data de un markdown, de un json. etc

se le puede explicar que atributos tiene la coleccion
import definecollection, z (para validar esquemas) from astro:content

definir la coleccion con el metodo

exportar collections = { books }

importar getcollection de astro:content

rutas dinamicas:
- /libro
	- [id].astro

website.com/libro/id

Componente ClientRouter para hacer transiciones

https://www.youtube.com/watch?v=WHqZAXHZN_w&t=2407s&ab_channel=midulive

- schemas
- paginas dinamicas
- plugin de tailwind paragraph
- ani maciones entre paginas
- variables de entorno
- server islands (para ejecutar js en el servidor y renderizar en el servidor, tambien usa fallbacks para renderizar algo mientras esta cargando)
- javascript en el cliente
- deploy
- pro tip variable de entorno

https://www.youtube.com/watch?v=RB5tR_nqUEw&t=1071s&ab_channel=midulive

### Curso Astro 3 Midu

INSTALAR EXTENSION DE ASTRO para los **.astro**

PLANTILLAS
astro build themes
astro build showcase
astroshipweb3templates

ESTRUCTURA DE CARPETAS
archivo de config astro, a la hora de crear integraciones es sencillo
src : componentes, layouts y paginas y env que es para recuperar el tipyng de castro

SINTAXIS
- los estilos tienen scope, solo afectan al componente que los contiene
- podes hacer estilos globales con etiqueta style is:global
- interface Props para tipar props que se reciben desde el padre

COMPONENTES

TAILWIND
```bash
#bash
npm astro add tailwind
```

ENRUTAMIENTO DE PAGINAS  / LAYOUT
con el sistema de archivos

SLOTS
el slot es como el children
usar slot names para indicar en que posicion renderizar el contenido https://youtu.be/RB5tR_nqUEw?t=2538

MARKDOWN


USAR HTML

FETCHING DE DATOS

RENDERIZADO CONDICIONAL DE ESTILOS
class:list = {Array}

GET STATIC PATHS
getStatisPaths()

SERVER SIDE RENDERING

COMPONENTES INTERACTIVOS
hace un componente de preact con un estado interno
llama al componente
le pone la directiva client:visible
si actualizo la pagina no hay persistencia de datos
para que haya persistencia de datos, hay que usar la directiva transition:persist. en el mismo componente o en un componente padre

