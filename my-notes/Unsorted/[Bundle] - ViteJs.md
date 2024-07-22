---
title: '[Bundle] - ViteJs'
created: '2022-12-29T16:32:52.374Z'
modified: '2023-01-14T16:53:26.528Z'
---

# [Bundle] - ViteJs

- Para crear proyecto de Vite : 
$npm create vite
- Dentro del proyecto : 
$npm install ó $npm i
- npm run build
- Ejecutar el proyecto en modo desarrollo : 
$npm run dev
- Convertir el código para producción : 
$npm run build
- Previsualizar el proyecto en producción : 
$npm run preview

#### Hostear en GitHub Pages :
- https://vitejs.dev/guide/static-deploy.html
- npm i gh-pages
- npm run build (para compilar todo en la carpeta dist)
- npx gh-pages -d dist (para subir la carpeta dist al host)

#### Importar imágenes : 
Importa la ruta del archivo luego de compilar la aplicación
```js
import URL_heart from'../img/heart.svg';
import URL_heartRed from'../img/heart-red.svg';
````







