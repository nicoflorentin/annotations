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

### 🪞Diff

- **Diff resumido entre ramas:** `git diff --stat main..feature-branch`
- **Log gráfico oneline:** `git log --oneline --graph --all --decorate`
- **Mostrar cambios de un commit especifico:** `git show <sha>`

### 🔀 Merge
- **Mergear una rama a la rama actual:** `git merge <branch>
- **Cancelar merge en proceso:** `git merge --abort`

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