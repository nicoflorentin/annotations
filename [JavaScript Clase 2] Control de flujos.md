---
tags: [Coderhouse, JavaScript]
title: '[JavaScript Clase 2] Control de flujos'
created: '2021-06-10T02:59:00.914Z'
modified: '2021-07-13T23:12:52.498Z'
---

# [JavaScript Clase 2] Control de flujos

## Condicionales

Cuando en programación hablamos de condicionales, hablamos de una estructura sintáctica que sirve para **tomar una decisión a partir de una condición**. 
Si <condición> entonces <operación>

### Estructura **IF**

La estructura más utilizada en la mayoría de los lenguajes, y por ende también en JS, es la **estructura if**.

```javascript
if (true){
    console.log("vas a ver este mensaje");
}
```

Si la condición se cumple (es decir, si su valor es true) se ejecutan todas las instrucciones que se encuentran dentro de {...}. Si la condición no se cumple (es decir, si su valor es false) no se ejecuta ninguna instrucción contenida en {...} y el programa continúa ejecutando el resto de instrucciones del script.

#### Ejemplo

```javascript
let unNumero = 5

// Con (unNumero == 5) comparamos si unNumero es igual a 5
if (unNumero == 5){
    console.log("vas a ver este mensaje");
}

// Con (unNumero == 6) comparamos si unNumero es igual a 6
if (unNumero == 6){ 
    console.log("no vas a ver este mensaje");
}
```

### Else

En ocasiones, las decisiones que se deben realizar no son del tipo "si se cumple la condición, hazlo; si no se cumple, no hagas nada". Normalmente las condiciones suelen ser del tipo **"si se cumple esta condición, hazlo; si no se cumple, haz esto otro"**.

```javascript
let unColor = "Rojo"

// Con (unColor == "Rojo") comparamos si unColor es igual "Rojo"
if (unColor == "Rojo"){
    console.log("el color es Rojo");
}else{
//La instrucción se interpreta cuando unColor NO es "Rojo"
    console.log("el color NO es Rojo");
}
```

### Condiciones anidadas [Else, If]

```javascript
let precio = 100.5;

if (precio < 20) {
    alert("El precio es menor que 20");
}
else if (precio < 50) {
    alert("El precio es menor que 50");
}
else if (precio < 100) {
    alert("El precio es menor que 100");
}
else {
    alert("El precio es mayor que 100");
}
   
```

## Variables booleanas

## True of False

L**as variables booleanas son las que sólo tienen dos valores, true or false.** Pueden recibir el valor a partir de una evaluación booleana sobre otras variables:

```javascript
let esValida = true;
let numero   = 10;
let esMayor5 = (numero > 5); // su valor sera true

if (esValida) {
    alert("Es boolean true");
}
```

## Operadores Lógicos

En JavaScript, disponemos de los operadores lógicos habituales en lenguajes de programación como son: es igual, es distinto, menor, menor o igual, mayor, mayor o igual, and (y), or (o) y not (no). 
La sintaxis se basa en símbolos, como veremos a continuación. Cabe destacar que hay que prestar atención a no confundir ‘==’ con ‘=’ porque implican distintas cosas.

| Operadores logicos y relacionales   | Descripción         |
| ----------                          | -----               |
| "==" | Es igual |
| "===" | Es estrictamente igual |
| "!=" | Es distinto |
| "!==" | Es estrictamente distinto |
| "<, <=, >, >=" | Menor, menor o igual, mayor, mayor o igual |
| "&&" | Operador And (y) |
| "||" | Operador or (o) |
| "!" | Operador not (no) |

## Condiciones compuestas con &&

```javascript
let nombreIngresado   = prompt("Ingresar nombre");
let apellidoIngresado = prompt("Ingresar apellido");

if((nombreIngresado !="") && (apellidoIngresado !="")){
    alert("Nombre: "+nombreIngresado +"\nApellido: "+apellidoIngresado); 
}else{
    alert("Error: Ingresar nombre y apellido");
}
```

## Condiciones compuestas por ||

En caso de utilizar || (OR), **será requisito que al menos una de las comparaciones sea verdadera para que la condición compuesta sea verdadera**.

```javascript
let nombreIngresado   = prompt("Ingresar nombre");

if((nombreIngresado == "ANA") || (nombreIngresado =="ana")){
    alert("El nombre ingresado es Ana"); 
}else{
    alert("El nombre ingresado NO ES Ana"); 
}
```


