---
tags: [CSS]
title: '[CSS] CSS fundamentals'
created: '2022-11-08T20:33:44.784Z'
modified: '2023-01-02T23:38:55.514Z'
---

# [CSS] CSS fundamentals

## Tamaños de pantalla :

```css
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...}

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...}

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...}

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {...}

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {...}
```

## Fuentes locales : 
```css
@font-face {
    font-family: LocalConsolas;
    src:url("../fonts/CONSOLA.TTF") ;
    font-weight: normal ;
    font-style: normal;
}
@font-face {
    font-family: LocalConsolas;
    src:url("/fonts/CONSOLAB.TTF");
    font-weight: bold;
    font-style: normal;
}
```

## Variables : 

Las variables globales se declaran en :root : 

```css
:root {
  --main-color: black;
}
```

Y se accede a ellas mediante la funcion var() :
```css
.class {
  color: var(--main-color);
}
```

## Optimal font sizes for **DESKTOP 💻** :

No hay reglas exactas pero si hay buenas practicas para tener en cuenta cuando se diseña en tamaño desktop.
- **Body text :** 16px a 18px. Hasta 21px
- **Headings :** 1.96 veces mas grande que el tamaño del Body text.
- **Subheadings :** Ligeramente mas pequeño que el tamaño del heading. Si el heading es de 35px entonces el subheading debe ser de 30px.
- **Input fields :** Debe coincidir ligeramente con las medidas del body text.

## Utilizar **em y rem** para el tamaño de la fuente : 

El tamaño default en los navegadores es de aproximadamente **16 pixels**. **Una práctica comun es configurar el root font size en 62.5%**. Que convierte el 16px por default a 10px. Para llegar a la igualdad de 1rem = 10px o 2.5rem = 25px. Asi cuando cambias la configuracion del root todos los tamaños de fuente configurados con rem se modificarán de acuerdo a las necesidades.

## Optimal font sizes for **MOBILE 📱** :

- Body text : 14px como mínimo (en los textos secundarios), hasta 16px. 
- Headings : 1.3 veces más grande que el body text.
- Subheadings : si el heading es de 23px entonces el sub debe ser de 18px o 16px. Pero con con una letra mas ligera.
- Input fields : Debe coincidir ligeramente con las medidas del body text.

## **Importante** : 
- Los margin bottom y top hacerlos absolutos, con pixeles. Para que no se deforme verticalmente entre dispositivos.
- Los margin left y right hacerlos con relativos para que sea responsivo.

## SVG Files : 
- Para que una imagen SVG configurada como background sea responsiva **borrar atributos height y width** del archivo svg
- Si tiene background-attachment: scroll; entonces usar background-size: cover;

## Unselectable text : 

```css
.unselectable {
   -moz-user-select: -moz-none;
   -khtml-user-select: none;
   -webkit-user-select: none;

   /*
     Introduced in IE 10.
     See http://ie.microsoft.com/testdrive/HTML5/msUserSelect/
   */
   -ms-user-select: none;
   user-select: none;
}
```

## Center a div : 
```css
.center {
    position:absolute;
    top:0;
    left:0;
    right:0;
    bottom:0;
    margin:auto;    
    width: 150px;
}
```
```css
.center {
    display: grid;
    place-content: center;
}
```


## CSS RESET : 

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
```

## CSS Specificity

1. **IMPORTANT**
2. **INLINE**
3. **ID NESTING**
4. **ID**
5. **CLASS NESTING**
6. **CLASS**
7. **TAG NESTING**
8. **TAG**

## ScrollBar style : 
```css
html {
	scrollbar-width: normal;
	scrollbar-color: red;
}
html::-webkit-scrollbar {
	width: 10px;
}
html::-webkit-scrollbar-thumb {
	background-color: #1C1C1C;
}
html::-webkit-scrollbar-thumb:hover {
	background-color: #464646;
}
html::-webkit-scrollbar-track {
	background-color: white;
}
```

## Prevent Dark Mode : 
```html
<meta name="color-scheme" content="light only">
<meta name="color-scheme" content="light dark">
```
o
```css
:root {
     color-scheme: light only;
}
```

## Text rendering : 
optimizeLegibility optimiza las letras muy juntas cuando el fontsize es menor a 20px : 
```css
:root {
text-rendering: auto;
text-rendering: optimizeSpeed;
text-rendering: optimizeLegibility;
text-rendering: geometricPrecision;
}
```

<<<<<<< HEAD:notes/[CSS] CSS fundamentals.md
## Reset an element style
```css
```css
/* basic modern patch */

#reset-this-root {
    all: unset;
}
```

or

```css
#reset-this-root {
    all: initial;
}
```
``
## White Space
The `white-space` property specifies how white-space inside an element is handled.
Lo usé para evitar que un texto en un título haga wrap y se desalinie del resto de los titulos adyacentes.
```css
.class {
white-space: normal|nowrap|pre|pre-line|pre-wrap|initial|inherit;
}
```

## ScrollBar and Layout
Evitar que cuando aparezca la scrollbar el layout se desplace a la izquierda
```css
/* tailwind class : className="w-screen" */
.container {
	width: 100vh;
}

/* alternative */
.container {
	position: relative; /* sin esta tambien funciona */
	padding-left: calc(100vw - 100%);
}
```

## Flexbox shortcut

## Tres elementos de distinto tamaño. Poner el item central en el centro del contenedor padre

TailwindCSS:
```html
<container className='flex-row grow gap-10'>
	<item1 className='grow basis-0'>12345678</item1>
	<item2>2</item2>
	<item3 className='grow basis-0'>3123</item3>
</container>
```
### Comparación

- **Tamaño Base:**
    
    - **`flex: 1 1 0`**: El tamaño base es `0`. El elemento no tiene un tamaño inicial y ocupa espacio solo en función del espacio disponible y el `flex-grow`.
    - **`flex: 1 1 auto`**: El tamaño base se ajusta automáticamente en función del contenido del elemento o de cualquier tamaño explícito que se haya establecido (como `width` o `height`).
- **Distribución del Espacio:**
    
    - **`flex: 1 1 0`**: El tamaño base es `0`, por lo que el elemento se expande para llenar el espacio disponible en el contenedor, ignorando el tamaño inicial.
    - **`flex: 1 1 auto`**: El tamaño base es determinado por el contenido o propiedades del elemento, y el espacio adicional se distribuye en base a `flex-grow`.
- **Uso:**
    
    - **`flex: 1 1 0`**: Útil cuando deseas que todos los elementos ocupen espacio en proporción al espacio disponible, ignorando sus tamaños base.
    - **`flex: 1 1 auto`**: Útil cuando deseas que los elementos respeten su tamaño base natural (determinado por su contenido o propiedades de tamaño) mientras aún se ajustan para llenar el espacio disponible.

Ambos enfoques tienen su utilidad dependiendo del diseño deseado y cómo quieres que los elementos se comporten dentro del contenedor flex.

resultado :
![[Pasted image 20240821230022.png]]

### min-height-size
Especifica el tamaño mínimo de un elemento en el eje del **bloque** de diseño lógico, que depende del flujo de contenido y el idioma.
```css
.box {
	min-height: 200px; /* Basado en altura fija (eje físico) */ 
	min-block-size: 200px; /* Basado en tamaño lógico adaptable */ 
}
```

## Inset

Espacio entre el elemento y su elemento padre, a diferencia del padding, el elemento hijo sera casi tan grande como el padre en todas sus dimensiones (x , y)
```css
/* CSS code*/
div {  
	inset: 35px;
}
```

## Auto scroll
```js
// autoScrollScript.js
const form = document.getElementById("form-surface-container")
const contactButton = document.getElementById("contact-button")

contactButton?.addEventListener("click", () => {
form?.scrollIntoView({ behavior: "smooth", block: "center" })
})
```
## To sort notes
saturation
w-auto- h-32