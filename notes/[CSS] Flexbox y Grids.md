---
tags: [Coderhouse, CSS]
title: '[CSS] Flexbox y Grids'
created: '2021-05-27T18:35:38.163Z'
modified: '2022-11-02T05:56:37.616Z'
---

# [CSS] Flexbox y Grids

## Flex container

```css
.flex-container {
  display: flex;
  propiedad: valor;
}
```

- **Distribuye elementos en vertical y horizontal**
- **Reordena la aparicion de elementos**
- **Redefine el sentido de flujo de los elementos**

## Elemento padre (Flex container)

- **display**: flex (el que inicia), indicará que sus hijos serán “flexibles”.
- **flex-direction**: elegir dirección vertical u horizontal.
- **flex-wrap**: ¿se hará multilínea cuando llegue al limite?
- **flex-flow**: abreviación de propiedades (flex-direction y flex-wrap)
- **justify-content**: alinear horizontalmente a los hijos si el padre es “fila” o verticalmente si el padre es “columna”
- **align-items:** alinea verticalmente a los hijos (si el padre es “fila”)
- **align-content**: alinea verticalmente a los hijos cuando son multilínea


### Propiedades del **contenedor**
  - **flex-direction:** column | column-reverse |  row | row-reverse
  - **flex-wrap:** wrap | wrap reverse
  - **flex-flow:** flex-direction | flex-wrap / **(método abreviado)**
  - **justify-content:** flex-start | flex-end | center | space-between | space-around
  - **align-items:** flex-start | flex-end | center | baseline
  - **align-content:** strech | flex-start | flex-end | center | space-between | space-around

### Propiedades de los **items**
  - **order:** integer
    - modifica el orden de aparición de un elemento
  - **flex-grow:** 0 | 1 | 2 | 3
    - tamaño del elemento con respecto a sus parientes
  - **flex-shrink:** 1 | 2 | 3
    - el elemento se encoge en caso que el máximo ancho sea alcanzado por los elementos
  - **flex-basis:** ancho | auto
    - define el ancho de un elemento inicial
  - **flex:** none | flex-grow flex-shrink flex-basis **(método abreviado)**
  - **align-self:** auto | stretch | center | flex-start | flex-end | baseline | initial | inherit
    - especifica la alineación del elemento seleccionado dentro del contenedor flexible

# Grids

Se destaca por dividir una página en regiones principales, o definir la relación en términos de tamaño, posición y capas, entre partes de un control.

## Propiedades del padre

En primer lugar, aplicas la propiedad **"display: grid"** al elemento padre.

### Filas y columnas explícitas

Es posible crear **cuadrículas con un tamaño definido**. Para ello, sólo tienes que usar las propiedades CSS **grid-template-columns y grid-template-rows**, las cuales sirven para indicar las dimensiones de cada celda de la cuadrícula, diferenciando entre columnas y filas.

```css
.grid {
   display: grid;  
				   /* 2 columnas */
   grid-template-columns: 300px 100px; 
   				   /* 2 filas */
   grid-template-rows: 40px 100px; 
}

```

```html
<section class="grid">
   <div>Item 1</div>
   <div>Item 2</div>
   <div>Item 3</div>
   <div>Item 4</div>
</section>

```

ó utilizar una unidad creada para ser usada en grid **( fr (fraction) )**
Nota: también es posible utilizar otras unidades y combinarlas, como porcentajes o la palabra clave auto (que obtiene el tamaño restante).


```css
.grid {
display: grid;  
	grid-template-columns: 2fr 1fr; 
	grid-template-rows: 3fr 1fr; 
}

```

### Filas y columnas repetitivas

Si necesitas hacer muchas columnas y filas iguales, puedes usar lo siguiente:

```css
.grid {
display: grid;  
	grid-template-columns: repeat(12, 1fr);
grid-template-rows: repeat(12, 1fr)
}

```

## Grid por áreas

Es posible indicar el nombre y la posición concreta de cada área de la cuadrícula. **Utiliza la propiedad grid-template-areas, donde debes especificar el orden de las áreas. Luego, en cada ítem hijo, usas la propiedad grid-area para indicar el nombre del área en cuestión.**

```html
<div id="grilla">
 	<header class="border">Header</header>
 	<section id="productos" class="border">Section</section>
 	<section id="servicios" class="border">Section</section>
 	<nav class="border">Navegacion</nav>
 	<aside class="border">Aside</aside>
 	<footer class="border">Pie de pagina</footer>
</div>
```

```css
#grilla {
   display: grid;
   grid-template-areas:
   "nav header header"
   "nav productos publicidad"
   "nav servicios publicidad"
   "nav footer footer";
   grid-template-rows: 100px 1fr 1fr 75px; 
   grid-template-columns: 20% auto 15%;
}
.border {
   border: 1px solid black;
}

```

```css
header {
   grid-area: header;
}
footer {
   grid-area: footer;
}
section#productos {
   grid-area: productos;     
}
section#servicios {
   grid-area: servicios;     
}
nav {
   grid-area: nav;
}
aside {
   grid-area: publicidad;
}

```

En la propiedad grid-template-areas **también es posible indicar una palabra clave especial:**
- La palabra clave none: Indica que no se colocará ninguna celda en esta posición.
- Uno o más puntos (.): Indica que se colocará una celda vacía en esta posición.

### Grid espacios

La cuadrícula tiene todas sus celdas una a continuación de la otra. Aunque sería posible **darle un margen a las celdas** dentro del contenedor.

```css
.grid {
   grid-column-gap: 10px;
   grid-row-gap: 15px;
}

```

### Posición de los hijos (desde el padre)

Es posible **distribuir los elementos** de una forma muy sencilla y cómoda: **justify-items y align-items**, que ya conocemos del módulo CSS Flexbox: 

- **justify-items:** start | end | center | stretch
  - Distribuye los elementos en el **eje horizontal**.
- **align-items:** start | end | center | stretch
  - Distribuye los elementos en el **eje vertical**.

```css
#padre {
  justify-items: stretch; /* start | end | center | stretch */
  align-items: stretch; /* start | end | center | stretch */
  display: grid;
  width: 95%;
  grid-template-columns: auto auto;
  grid-column-gap: 10px;
  grid-template-rows: 100px 100px;
  grid-row-gap: 10px;
}
```

```css
#padre div {
  border: solid 1px;
  font-size: 21px;
  padding: 5px;
  background-color: yellow;
}
```

### Posición de los elementos

Es posible utilizar las propiedades **justify-content o align-content** para cambiar la distribución de todo el contenido en su conjunto.

- **justify-content:** start | end | center | stretch | space-around | space-between | space-evenly
  - Distribuye los elementos en el **eje horizontal**.
- **align-content:** start | end | center | stretch | space-around |space-between | space-evenly
  - Distribuye los elementos en el **eje vertical**.

## Propiedades de los ITEMS

Hay ciertas propiedades que **se aplican a cada ítem hijo de la cuadrícula**, para alterar o cambiar el comportamiento específico de dicho elemento.

- **justify-self**: start | end | center | strech 
  - Altera la justificación del ítem hijo en el eje horizontal.
- **align-self**: start | end | center
  - Altera la alineación del ítem hijo en el eje vertical.
- **grid-area**
  -Indica un nombre al área especificada, **para su utilización con grid-template-areas.**

  Existen algunas propiedades más, referentes en este caso, a la posición de los hijos de la cuadrícula donde va a comenzar o terminar una fila o columna. Las propiedades son las siguientes:

- **grid-column-start:** | integer |
  - Indica en qué columna empezará el ítem de la cuadrícula.
- **grid-column-end:**| integer |
  - Indica en qué columna terminará el ítem de la cuadrícula.
- **grid-row-start:** | integer |
  - Indica en qué fila empezará el ítem de la cuadrícula.
- **grid-row-end:** | integer |
  - Indica en qué fila terminará el ítem de la cuadrícula.





