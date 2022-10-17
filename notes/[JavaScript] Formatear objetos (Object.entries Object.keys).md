---
tags: [JavaScript]
title: '[JavaScript] Formatear objetos (Object.entries Object.keys)'
created: '2022-10-06T22:12:01.290Z'
modified: '2022-10-08T19:10:37.475Z'
---

# [JavaScript] Formatear objetos (Object.entries Object.keys)

```js
let formattedBreeds = Object.entries(formattedData).map((entry , index) => {
  const [breed, arr] = entry;
  const subBreed = arr[0]
  return {    
    breed,
    subBreed,
    id: index
  }
});
```

