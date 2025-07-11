## Comandos

### 🪴 Ramas

- **Ver ramas:** `git branch`
- **Mostrar todas las ramas (locales + remotas):** `git branch -a`
- **Cambiar de rama:** `git checkout nombreDeRama`
- **Eliminar rama local:** `git branch -d branch-name`
- **Eliminar rama remota:** `git push origin --delete nombreDeRama`
- **Actualizar ramas remotas (y limpiar las borradas):** `git fetch --prune`

### 🔁 Tracking

- **Descargar cambios sin fusionar:** `git fetch origin`
- **Commit vacío (sin modificar archivos):** `git commit --allow-empty -m "Mensaje del commit"`
- **Eliminar archivos y directorios no trackeados:** `git clean -df`
- **Eliminar solo directorios no trackeados:** `git clean -d`
- **Eliminar solo archivos no trackeados:** `git clean -f`

### 🚀 Push

- **Subir la rama y setear tracking:** `git push -u origin <branchName>`
- **Forzar push (sobrescribir remoto):** `git push --force`

### 📥 Pull
- **Pull equivale a:** `git fetch && git merge`
- **Pull sin commit automático:** `git pull --no-commit origin main`
- **En lugar de hacer merge, reubica tus commits encima de los que vienen del remoto:** `git pull --rebase`
- **Si trabajás en ramas activamente modificadas por otros, en lugar de `git pull`, hacé:** `git fetch git && rebase origin/main`
### 🔙 Reset

- **Soft reset (mantiene staged):** `git reset --soft HEAD~1` — deshace el último commit pero deja archivos en staging.
- **Mixed reset (unstaged):** `git reset --mixed HEAD~1` — deshace el último commit y deja cambios sin staging.
- **Hard reset (borra todo):** `git reset --hard HEAD~1` — deshace último commit y elimina cambios locales.

### Diff

- **Diff resumido entre ramas:** `git diff --stat main..feature-branch`
- **Log gráfico oneline:** `git log --oneline --graph --all --decorate`
- **Mostrar cambios de un commit especifico:** `git show <sha>`

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

git checkout -b new-branch-name

### Git merge
Habiendo trabajado en diferentes ramas deberíamos de mezclarlas. Lo primero que debemos hacer para mezclar ramas es pararnos sobre la rama master y desde allí usar el comando git merge {rama a fundir con el master}
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

## Apunte de GIT henry :

### Clone

Un "clone" (clon) en Git se refiere a la acción de crear una copia exacta de un repositorio remoto en tu máquina local. Puedes clonar un repositorio utilizando el comando `git clone` seguido de la URL del repositorio remoto. Al clonar un repositorio, obtienes una copia completa del historial de commits, ramas y archivos en tu propia máquina. **Esto te permite trabajar en el repositorio localmente y realizar cambios sin afectar el repositorio remoto. Además, puedes sincronizar tu repositorio clonado con el repositorio remoto para obtener actualizaciones utilizando comandos como** `**git pull**` **y** `**git push.**`

### Pull y Push

1. **"git pull":** Este comando se utiliza para obtener y fusionar los cambios más recientes desde un repositorio remoto en tu repositorio local. Básicamente, **realiza dos acciones en una sola operación: primero, descarga las actualizaciones del repositorio remoto utilizando "git fetch" y luego fusiona esos cambios en tu rama actual.** Es importante destacar que si tienes cambios locales sin confirmar, Git intentará fusionar los cambios remotos con tus cambios locales. En caso de que haya conflictos, deberás resolverlos manualmente. El comando "git pull" se utiliza comúnmente para mantener tu repositorio local actualizado con los últimos cambios del repositorio remoto.
2. **"git push":** Este comando se utiliza para enviar tus cambios locales a un repositorio remoto. **Cuando realizas cambios en tu repositorio local y estás listo para compartirlos con otros colaboradores o actualizar el repositorio remoto, utilizas "git push". Git enviará tus cambios al repositorio remoto correspondiente y los integrará en la rama apropiada.** Es importante destacar que debes tener permisos de escritura en el repositorio remoto para poder utilizar "git push". Si otros colaboradores han realizado cambios en el repositorio remoto desde la última vez que hiciste "git pull" o "git clone", es posible que se produzcan conflictos, y deberás resolverlos antes de que Git pueda realizar el "push" correctamente.

**En resumen,**
**"git pull" se utiliza para obtener y fusionar los cambios remotos en tu repositorio local**
**"git push" se utiliza para enviar tus cambios locales al repositorio remoto.**

## Flujo de trabajo con Git (Git Flow)

### Paso a paso para hacer un pull request y subir un cambio a nuestra rama principal (main).

1. **git checkout main:** nos posicionamos en la rama main.
2. **git branch:** vemos todas las ramas creadas (opcional).
3. **git pull:** nos traemos todos los últimos cambios que hayan sido mergeados y aprobados en main. Sobre este comando, también tenemos la posibilidad de usar **git pull origin nombreRama** para traernos los cambios de la rama especificada.
4. **git checkout -b nombreRama:** estando posicionados en main, creamos una nueva rama. Es importante crear una nueva rama para cada nueva feature/fix así nos evitamos conflictos.
5. Realizamos los cambios estando posicionados en la rama previamente creada.
6. **git status:** vemos que archivos fueron modificados y están listos para ser agregados a un nuevo commit.
7. **git add nombreDeArchivoModificado:** añadimos el archivo indicado al nuevo commit. En este caso, si tenemos más de un archivo modificado y queremos añadir a todos, podemos hacer git add . con el punto al final para poder añadirlos todos juntos y no ir archivo por archivo.
8. **git push -u origin nombreRamaDeTrabajo:** subimos los cambios a la rama remota del repositorio. Por ejemplo, si mi rama creada en el paso 4 de esta lista se llamaba feature/login en este paso el comando debería ser **git push -u origin feature/login.**
9. Una vez realizados los pasos anteriores, se abre la posibilidad de hacer un pull request. Para ésto, debemos ir al repositorio en GitHub y hacer click en el botón de color verde que dice **“CREATE PULL REQUEST”.**
10. Uno (o varios) de los colaboradores del repositorio debe aceptar los cambios.
11. Una vez que los cambios son aceptados, hacer click en el botón **“CONFIRM SQUASH AND MERGE”.** Ésto genera que nuestros cambios ahora se vean reflejados en la rama main.
12. Si queremos, ahora podemos **borrar la rama creada para ésta tarea en particular.**
13. Para realizar una nueva tarea, el ciclo se repite. Aclaración: tener en cuenta que el orden de los comandos puede verse afectado dependiendo de lo que se quiera realizar.

## Trabajo en equipo

1. **Agregar colaboradores** desde al configuracion del repositorio.
2. **Proteger las ramas** con reglas de proteccion desde la configuracion de Branches protection rules.
3. **Pushear** los cambios a la nueva rama.
4. Generar un **pull request.**
5. Una vez aceptado se puede hacer **merge** a la rama principal.