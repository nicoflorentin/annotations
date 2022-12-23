---
tags: [Coderhouse]
title: Git y GitHub
created: '2022-10-04T18:32:08.564Z'
modified: '2022-11-22T06:55:51.463Z'
---

# Git y GitHub

## Comandos : 

### Configurar nombre y email : 

git config --global user.name "John Doe"
git config --global user.email johndoe@example.com

### Comprobar configuración : 

git config --list
git config user.name

### Comprobar ayuda, 3 métodos :

$ git help config 
$ git config --help
$ man git-config 

###  Comandos de la consola de Windows : 

Hay que tener varias cosas en cuenta:
- No diferencia entre mayúsculas y minúsculas
- Al escribir un nombre de archivo o carpeta con espacios conviene escribirlo entrecomillado
- Los nombres pueden ser de hasta 255 caracteres y con extensiones de hasta 3 caracteres * Si eliminas un archivo desde CMD no va a la Papelera.

/? Si quieres saber más de un comando, añade /? para ver la ayuda relacionada. Te será muy útil para ver las muchas opciones de cada comando.
HELP Te mostrará una lista de comandos disponibles.
DIR Es el comando más conocido de DOS y sirve para ver el contenido de una carpeta.
(en MAC-OS usar LS)
CD Sirve para entrar en una carpeta o salir de ella con CD…
CLEAR limpiar consola
MKDIR Con este comando crearás una carpeta nueva. Con RMDIR podrás eliminarla.
MOVE y COPY Son los comandos para mover y copiar respectivamente archivos. Deberás indicar el nombre del archivo con su ruta (si está en otra carpeta en la que te encuentras) y la ruta de destino.
RENAME Sirve para renombrar un archivo o carpeta. Hay que indicar el nombre original y el definitivo.
DEL Es el comando para eliminar un archivo. Recuerda que no irá a la Papelera, así que piénsatelo antes de borrar nada. Y para eliminar carpeta usa el comando RD (en MAC-OS usar RM para archivos / para eliminar carpetas RM -RF)
EXIT Cierra la ventana de la línea de comandos o símbolo del sistema.
COPY CON Crear archivos. (en MAC-OS usar TOUCH)

## Utilizando Git : 

### Crear repositorio : git init

john@MyShopSolutions MINGW64 /c/git
$ git init nuevo_repo
ó
john@MyShopSolutions MINGW64 /c/git
$ mkdir nuevo_repo
$ git init

### Ver el estado de los archivos locales (Working Directory): git status

Creando un archivo index.html
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ touch index.html

Ver el estado de los archivos locales : 
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git status

### Agregar archivos al Staging Area : git add

john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git add index.html

### Comitear archivos : git commit
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git commit -m "nuevo archivo"

### Ver la historia del proyecto :
$ git log

### Comparar commits : 
Git diff
Lo primero es obtener los números de commit a comparar, podemos usar el comando git log --oneline (para ver los commits en su versión corta)
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git log --oneline
95bd15b (HEAD -> master) nuevos cambios
1734915 nuevo archivo

#### Podemos ver las diferencias entre las versiones del documento utilizando git diff [version 1] [version 2] : 
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git diff 1734915 95bd15b

#### Git branch
Este comando lo usaremos para crear una nueva rama o un nuevo branch.
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git branch responsive

Vamos ahora a listar nuestras ramas con el comando git branch -l
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git branch -l
* master
  responsive

Aparece un listado con nuestras ramas (la rama principal -master-) 

#### Borrar Ramas : 
// delete branch locally
git branch -d localBranchName
// delete branch remotely
git push origin --delete remoteBranchName

Para borrar una rama usamos el comando git branch -D [nombre de la rama]
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git branch -D responsive
Deleted branch responsive (was 6d6c28c)

Volvemos a crear una nueva rama y esta vez vamos a renombrarla con el comando git branch -m [nombre de la rama] [nombre nuevo de la rama]
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git branch features
$ git branch -m features f-responsive

### Git checkout
Ahora vamos a ver con que comando podemos movernos entre nuestras diferentes ramas y posicionarnos en una como en otra para empezar a trabajar sobre ellas.
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git checkout f-responsive

Luego de ejecutar el comando estaríamos trabajando sobre la rama indicada (en este caso “f-responsive”)

También podríamos movernos y posicionarnos sobre algún commit específico y desde allí sacar una nueva rama

Primero buscamos y listamos los commits (usamos el comando git log --oneline, para que nos haga una lista de los commits con sus identificadores en su versión corta)
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git log --oneline
6d6c28c (HEAD -> master, f-responsive) Agregue una línea en la cuarta posición
95bd15b nuevos cambios
1734915 nuevo archivo

Luego con el comando checkout nos posicionamos sobre el commit que seleccionamos
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git checkout 95bd15b
Note: checking out '95bd15b'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

git checkout -b <new-branch-name>

### Git merge
Habiendo trabajado en diferentes ramas deberíamos de mezclarlas. Lo primero que debemos hacer para mezclar ramas es pararnos sobre la rama master y desde allí usar el comando git merge [rama a fundir con el master]
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git merge nueva-image
Updating 6d6c28c..fa52a3c
Fast-forward
 nuevo.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 nuevo.txt

Ahora los cambios de nuestra rama “nueva-imagen” fueron fundidos a nuestra rama “master”

### Ver el arbol del proyecto : --graph
Con el comando git  log --oneline --graph podremos ver la bifurcaciones de nuestro proyecto con sus respectivas y diferentes ramas y como se fueron fusionando con nuestra rama master. 
john@MyShopSolutions MINGW64 /c/git/nuevo_repo (master)
$ git log --oneline --graph
* 3bb3eac (HEAD -> master) Nuevo cambio
*   db7e9e8 Mix merge de cambios
|\
| * 054f907 (nueva-imagen) Nueva línea de nueva imagen
* |   5c6788d Nuevo cambio por conflicto
|\ \
| * | 8bdde3d (f-responsive) Nueva línea de responsive
* | | 54617a6 Nueva línea
* | | 0e45eb0 Nuevo archivo en el master
|/ /
* | fa52a3c Nuevo en nueva rama
|/
* 6d6c28c Agregue una línea en la cuarta posición
* 95bd15b Nuevos cambios
* 1734915 Nuevo archivo







