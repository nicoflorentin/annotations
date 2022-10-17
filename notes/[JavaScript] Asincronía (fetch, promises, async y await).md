---
tags: [JavaScript]
title: '[JavaScript] Asincronía (fetch, promises, async y await)'
created: '2022-04-05T05:11:36.111Z'
modified: '2022-09-30T02:58:10.574Z'
---

# [JavaScript] Asincronía (fetch, promises, async y await)

## Fetch()

A promise is an **object** returned by an asynchronous function

```javascript
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

console.log(fetchPromise);

fetchPromise.then( response => {
  console.log(`Received response: ${response.status}`);
});

console.log("Started request...");
```

With the fetch() API, once you get a Response object, you need to call another function to get the response data. In this case we want to get the response data as JSON, **so we would call the json() method of the Response object**. It turns out that **json() is also asynchronous**. So this is a case where we have to call two successive asynchronous functions.

Try this:
```js
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
fetchPromise.then( response => {
  const jsonPromise = response.json();
  jsonPromise.then( json => {
    console.log(json[0].name);
  });
});
```
Another way to code:
```js
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

fetchPromise
  .then( response => {
    return response.json();
  })
  .then( json => {
    console.log(json[0].name);
  });
```

## Combining multiple promises ##

Sometimes you need all the promises to be fulfilled, but they don't depend on each other. In a case like that it's much more efficient to start them all off together, then be notified when they have all fulfilled. **The Promise.all() method is what you need here. It takes an ARRAY OF PROMISES, and returns a single promise.**

The promise returned by **Promise.all([array])** is:

- fulfilled :  **when and if all the promises in the array are fulfilled**. In this case the then() handler is called with an array of all the responses, in the same order that the promises were passed into all()
- rejected : **when and if any of the promises in the array are rejected**. In this case the catch() handler is called with the error thrown by the promise that rejected.
For example:
```js
const fetchPromise1 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
const fetchPromise2 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found');
const fetchPromise3 = fetch('https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json');

Promise.all([fetchPromise1, fetchPromise2, fetchPromise3])
  .then( responses => {
    for (const response of responses) {
      console.log(`${response.url}: ${response.status}`);
    }
  })
  .catch( error => {
    console.error(`Failed to fetch: ${error}`)
  });
```

**Sometimes you might need any one of a set of promises to be fulfilled, and don't care which one. In that case you want Promise.any()**. This is like Promise.all(), except that **it is fulfilled as soon as any of the array of promises is fulfilled, or rejected if all of them are rejected:**

const fetchPromise1 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
const fetchPromise2 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found');
const fetchPromise3 = fetch('https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json');
```js
Promise.any([fetchPromise1, fetchPromise2, fetchPromise3])
  .then( response => {
    console.log(`${response.url}: ${response.status}`);
  })
  .catch( error => {
    console.error(`Failed to fetch: ${error}`)
  });
```
Note that in this case we can't predict which fetch request will complete first.


## setTimeout()

setTimeout(callback , miliseconds)
ej:

```js
function asyncFunction (a,b) => {
  setTimeout( () => {
    return a + b
  },5000)
}

asyncFunction(1,2)

```

## Promises

```js
const promesa = new Promise( (resolve, reject) => {
  if (x=1) {
    resolve('chain')
  } else {
    reject('reject chain')
  }
})

promesa
  .then(res => console.log("resuelto!" + res))
  .catch(err => console.log("error!" + err))
```


Async Javascript Tutorial For Beginners (Callbacks, Promises, Async Await):
https://www.youtube.com/watch?v=_8gHHBlbziw&t=10s&ab_channel=DevEd

### método promise.resolve()
El método Promise.resolve(value) retorna un objeto Promise que es resuelto con el valor dado.
```js
const funcion = () => {
	return Promise.resolve('resuelto!')
}
let resultado = funcion().then((res) => {
	console.log(res)
})
//output : "resuelto!"
```

## Async - Await

Adding async at the start of a function makes it an async function: **Hace que la funcion retorne una promesa**


```js
async function myFunction() {
  // This is an async function
}
```

Inside an async function you can use the **AWAIT KEYWORD before a call to a function that returns a promise**
**THIS MAKE THE CODE WAIT AT THAT POINT UNTIL THE PROMISE IS SETTLED**
at which point the fulfilled value of the promise is treated as a return value, or the rejected value is thrown.

This enables you to write code that uses asynchronous functions but **looks like synchronous code**. For example, we could use it to rewrite our fetch example:
```js
async function fetchProducts() {
  try {
    // after this line, our function will wait for the `fetch()` call to be settled
    // the `fetch()` call will either return a Response or throw an error
    const response = await fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    // after this line, our function will wait for the `response.json()` call to be settled
    // the `response.json()` call will either return the JSON object or throw an error
    const json = await response.json();
    console.log(json[0].name);
  }
  catch(error) {
    console.error(`Could not get products: ${error}`);
  }
}

fetchProducts();
```
Here we are calling await fetch(), and instead of getting a Promise, our caller gets back a fully complete Response object, just as if fetch() were a synchronous function!

We can even use a try...catch block for error handling, exactly as we would if the code were synchronous.
```js
async function fetchProducts() {
  try {
    const response = await fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    const json = await response.json();
    return json;
  }
  catch(error) {
    console.error(`Could not get products: ${error}`);
  }
}

const jsonPromise = fetchProducts();
jsonPromise.then((json) => console.log(json[0].name));
```

You'll probably use async functions a lot where you might otherwise use promise chains, and they make working with promises much more intuitive.

**Tener en cuenta que como sucede en las cadenas de promesas, await fuerza que las operaciones asincronas se completen en series, esto es necesario si el resultado de la próxima operación depende del resultado de la última, pero si éste no es el caso entonces Promise.all() sera mas adecuado.**

### Segundo parámetro del fetch():

El método fetch puede recibir un **segundo prámetro, un objeto que te permite controlar distintas configuraciones:**

```js
fetch('https://example.com/profile',
  {
    method: 'POST', // or 'PUT'
    headers:
      {
        'Content-Type': 'application/json',
      },
    body: JSON.stringify(data),
})
```

### Hacer fetch() a múltiples URLs : 

```js
async function getAllURLs(urls) {
  try {
    var data = await Promise.all(
      urls.map((url)=>{
        fetch(url).then(
          response => response.json()
        )})
    );

    return data
  } catch (error) {
    console.log(error)
    throw (error)
  }
}

///o si no tambien : 

Promise.all([1, 2, 3].map(id => 
  fetch(`https://jsonplaceholder.typicode.com/todos/${id}`).then(resp => resp.json())
)).then(console.log);
```

