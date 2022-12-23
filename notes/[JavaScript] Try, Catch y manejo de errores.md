---
tags: [JavaScript]
title: '[JavaScript] Try, Catch y manejo de errores'
created: '2022-09-29T04:04:57.860Z'
modified: '2022-12-21T05:28:22.713Z'
---

# [JavaScript] Try, Catch y manejo de errores

- try : Define el bloque de código que se ejecuta
- catch(err) : Define el bloque de código que se ejecuta para manejar el error
- finally : Define el bloque de código que se ejecuta sin importar el resultado del try
- throw "var" : Define un error personalizado

catch y finally son opcionales, pero si o si hay que usar uno o el otro.

La instrucción **throw lanza una excepción definida por el usuario. La ejecución del bloque try se detendrá (las declaraciones posteriores a throw no se ejecutarán) y el control pasará al primer bloque catch en la pila de llamadas**. Si no existe ningún bloque catch entre las funciones de llamada, el programa terminará.

Use la instrucción **throw para lanzar una excepción**. Cuando lanza una excepción, la expresión especifica el valor de la excepción. Cada uno de los siguientes arroja una excepción:

```js
throw "big"
throw 100
throw person
throw false
throw new Error('chain')
```

Ejemplo : 
```js
const errorFunction = (num) => {
  return new Promise ((resolve,reject)=>{
    console.log('resolviendo promesa en 1 segundo')
    setTimeout( () => {
      if(num){
        resolve(num)
      } else {
        reject(new Error('no hay ningun numero') )
      }
    },1000)
  })
}

const tryFunction = async () => {

  try {
    let error = await errorFunction(null)
    .then((res)=>{console.log(res)})
    .catch((err)=>{
      return err
    })
  
    throw new Error(error.message)
  
  } catch(error) {
    alert(error.message)
  }
}

tryFunction()
```


