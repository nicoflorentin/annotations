---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 3] Ciclos e Iteraciones'
created: '2021-06-10T13:52:54.388Z'
modified: '2021-07-13T23:12:44.317Z'
---

# [JavaScript Clase 3] Ciclos e Iteraciones

## Ciclos

Los ciclos, también conocidos como bucles o iteraciones son un medio rápido y sencillo para hacer algo **repetidamente**.
Si tenemos que hacer alguna operación más de una vez en el programa, de forma consecutiva, usaremos las estructuras de bucles de JavaScript:  **for, while o do..while**

### Tipos de bucles

- CICLOS POR CONTEO
Repiten un bloque de código un número de veces específica. Estructura **for**.

- CICLOS CONDICIONALES
Repiten un bloque de código mientras la condición evaluada es verdadera. Estructuras **while y do...while**.

#### Estructura FOR

```javascript
for(desde; hasta; actualización) {
 … //lo que se escriba acá se ejecutará mientras dure el ciclo
}
```

El **"desde"** es la zona en la que se establecen los valores iniciales de las variables que controlan el ciclo.
El **"hasta"** es el único elemento que decide si se repite o se detiene el ciclo.
La "actualización" es el nuevo valor que se asigna después de cada repetición a las variables que controlan la repetición.

Ejemplo:

```javascript
for (let i = 0; i <= 10; i++) {
    alert(i);
}
```

#### Sentencia BREAK

A veces, cuando escribimos una estructura for, necesitamos que bajo cierta condición el ciclo se interrumpa. Para eso se utiliza la sentencia break;
Al escribir esa línea dentro de un ciclo for, **el mismo se interrumpirá como si hubiera finalizado.**

```javascript
for (let i = 1; i <= 10; i++) {
    //Si la variable i es igual 5 interrumpo el for. 
    if(i == 5){
        break;
    }
    alert(i);
}
```

#### Sentencia CONTINUE

A veces, cuando escribimos una estructura for, necesitamos que bajo cierta condición, **el ciclo saltee esa repetición y siga con la próxima**. Para eso se utiliza la sentencia continue.

```javascript
for (let i = 1; i <= 10; i++) {
    //Si la variable i es 5, no se interpreta la repetición
    if(i == 5){
        continue;
    }
    alert(i);
}
```

#### Sentencia WHILE

La estructura while permite crear bucles que se ejecutan ninguna o más veces, dependiendo de la condición indicada.
El funcionamiento del bucle while se resume en: **mientras se cumpla la condición indicada, repite indefinidamente las instrucciones incluidas dentro del bucle.**

```javascript
let entrada = prompt("Ingresar un dato");
//Repetimos con While hasta que el usuario ingresa "ESC"
while(entrada != "ESC" ){
    alert("El usuario ingresó "+ entrada);
    //Volvemos a solicitar un dato. En la próxima iteración se evalúa si no es ESC.
    entrada = prompt("Ingresar otro dato");
}
```

#### Sentencia DO - WHILE

La estructura do..while permite crear bucles que se ejecutan una o más veces, dependiendo de la condición indicada.
**A diferencia de while, garantiza que el bloque de código se interpreta al menos una vez, porque la condición se evalúa al final.**

```javascript
let numero = 0;
do {
   //Repetimos con do...while mientras el usuario ingresa un n°
   numero = prompt("Ingresar Número");
   console.log(numero);
//Si el parseo no resulta un número se interrumpe el bucle.   
}while(parseInt(numero));
```

#### Estructura SWITCH

La estructura switch está especialmente diseñada para manejar de forma sencilla múltiples condiciones sobre la misma variable (técnicamente se podría resolver con un if, pero el uso de switch es más ordenado). Su definición formal puede parecer confusa, pero veamos un ejemplo para entender su simpleza.

- Cada condición se evalúa y si se cumple, se ejecuta lo que esté indicado adentro.

- Normalmente, después de las instrucciones de cada case se incluye la sentencia break para terminar la ejecución del switch, aunque no es obligatorio.

- ¿Qué sucede si ningún valor de la variable del switch coincide con los valores definidos en los case? 

- En este caso, se utiliza el valor default para indicar las instrucciones que se ejecutan cuando ninguna condición anterior se cumplió.

Ejemplo:

```javascript
let entrada = prompt("Ingresar un nombre");
//Repetimos hasta que se ingresa "ESC"
while(entrada != "ESC" ){
   switch (entrada) {
       case "ANA":
            alert("HOLA ANA");
            break;
        case "JUAN":
            alert("HOLA JUAN");
            break;
       default:
           alert("¿QUIÉN SOS?")
           break;
   }
   entrada = prompt("Ingresar un nombre");
}
```
