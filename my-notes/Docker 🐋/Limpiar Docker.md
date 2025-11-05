### 🧹 1. Ver qué hay antes de limpiar (opcional)

```bash
docker ps -a          # Lista todos los contenedores (incluso parados)
docker images         # Lista todas las imágenes
docker volume ls      # Lista los volúmenes
docker network ls     # Lista las redes
```

---

### 💀 2. Parar y eliminar todos los contenedores

```bash
docker stop $(docker ps -aq) 2>/dev/null
docker rm $(docker ps -aq) -f 2>/dev/null
```

---

### 🧨 3. Eliminar todas las imágenes

```bash
docker rmi $(docker images -q) -f 2>/dev/null
```

---

### 🧯 4. Eliminar todos los volúmenes

```bash
docker volume rm $(docker volume ls -q) -f 2>/dev/null
```

---

### 🔥 5. Eliminar todas las redes personalizadas

_(no borra las de sistema: bridge, host, none)_

```bash
docker network rm $(docker network ls -q) 2>/dev/null
```

---

### 🧘‍♂️ 6. Limpiar caché y datos huérfanos

```bash
docker system prune -a --volumes -f
```

> ⚠️ `-a` borra **imágenes no usadas**  
> ⚠️ `--volumes` borra **volúmenes no referenciados**

---

### ✅ 7. Confirmar que quedó vacío

```bash
docker system df    # Muestra uso de espacio
docker ps -a        # No debería mostrar nada
docker images       # Vacío
docker volume ls    # Vacío
```

---

💡 Si usás **Docker Compose**, también podés limpiar desde ahí:

```bash
docker compose down --volumes --rmi all
```
