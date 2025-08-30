# Comandos Docker - Guía Completa

## 🚀 **COMANDOS BÁSICOS**

### **Información del Sistema**

```bash
docker --version           # Versión de Docker
docker info                # Información detallada del sistema
docker system df           # Uso de espacio en disco
docker system events       # Ver eventos en tiempo real
```

### **Gestión de Imágenes**

```bash
# Descargar imágenes
docker pull ubuntu:22.04
docker pull nginx:latest

# Listar imágenes
docker images              # Ver todas las imágenes
docker images -a           # Incluir imágenes intermedias

# Eliminar imágenes
docker rmi imagen_id       # Eliminar una imagen
docker rmi $(docker images -q)  # Eliminar todas las imágenes
```

### **Gestión de Contenedores**

```bash
# Ejecutar contenedores
docker run hello-world              # Ejecutar y salir
docker run -it ubuntu bash          # Interactivo con terminal
docker run -d nginx                 # En segundo plano (detached)
docker run -p 8080:80 nginx         # Con puerto mapeado
docker run --name mi_nginx nginx    # Con nombre personalizado

# Listar contenedores
docker ps                  # Contenedores ejecutándose
docker ps -a              # Todos los contenedores
docker ps -q              # Solo IDs

# Controlar contenedores
docker start contenedor_id    # Iniciar contenedor parado
docker stop contenedor_id     # Parar contenedor
docker restart contenedor_id  # Reiniciar contenedor
docker pause contenedor_id    # Pausar contenedor
docker unpause contenedor_id  # Reanudar contenedor

# Eliminar contenedores
docker rm contenedor_id       # Eliminar contenedor parado
docker rm -f contenedor_id    # Forzar eliminación
docker rm $(docker ps -aq)   # Eliminar todos los contenedores
```

### **Interactuar con Contenedores**

```bash
# Acceder a contenedores en ejecución
docker exec -it contenedor_id bash
docker exec -it contenedor_id /bin/sh

# Ver logs
docker logs contenedor_id
docker logs -f contenedor_id     # Seguir logs en tiempo real
docker logs --tail 50 contenedor_id  # Últimas 50 líneas

# Ver procesos
docker top contenedor_id

# Inspeccionar contenedores
docker inspect contenedor_id
```

---

## 🔥 **COMANDOS INTERMEDIOS**

### **Volúmenes y Almacenamiento**

```bash
# Crear volúmenes
docker volume create mi_volumen

# Listar volúmenes
docker volume ls

# Usar volúmenes
docker run -v mi_volumen:/app/data nginx
docker run -v /host/path:/container/path nginx  # Bind mount

# Eliminar volúmenes
docker volume rm mi_volumen
docker volume prune              # Eliminar volúmenes no usados
```

### **Redes**

```bash
# Listar redes
docker network ls

# Crear red personalizada
docker network create mi_red

# Conectar contenedor a red
docker run --network mi_red nginx
docker network connect mi_red contenedor_id

# Inspeccionar red
docker network inspect mi_red

# Eliminar redes
docker network rm mi_red
docker network prune
```

### **Dockerfile y Construcción**

```bash
# Construir imagen desde Dockerfile
docker build -t mi_imagen:tag .
docker build -f Dockerfile.dev -t mi_imagen:dev .

# Ver historial de construcción
docker history imagen_id

# Etiquetar imágenes
docker tag imagen_id mi_repo/mi_imagen:v1.0
```

### **Registry y Repositorios**

```bash
# Subir/bajar imágenes
docker push mi_usuario/mi_imagen:tag
docker pull mi_usuario/mi_imagen:tag

# Login en registry
docker login
docker login registry.example.com

# Buscar imágenes
docker search ubuntu
```

---

## ⚡ **COMANDOS AVANZADOS**

### **Docker Compose**

```bash
# Gestión de servicios múltiples
docker-compose up -d           # Levantar servicios
docker-compose down            # Bajar servicios
docker-compose ps              # Ver servicios
docker-compose logs -f         # Ver logs
docker-compose exec web bash   # Ejecutar comando en servicio
docker-compose scale web=3     # Escalar servicio
```

### **Monitoreo y Estadísticas**

```bash
# Estadísticas en tiempo real
docker stats                   # Todos los contenedores
docker stats contenedor_id     # Contenedor específico

# Uso de recursos
docker system df -v            # Detalles de uso de espacio

# Procesos del sistema
docker system events --since 1h
```

### **Gestión Avanzada de Imágenes**

```bash
# Construcción multi-stage
docker build --target desarrollo -t mi_app:dev .

# Construcción con argumentos
docker build --build-arg VERSION=1.0 -t mi_app .

# Cache de construcción
docker build --no-cache -t mi_app .
docker builder prune              # Limpiar cache de build
```

### **Contenedores con Configuración Avanzada**

```bash
# Límites de recursos
docker run -m 512m --cpus="1.5" nginx

# Variables de entorno
docker run -e VAR1=valor1 -e VAR2=valor2 nginx
docker run --env-file .env nginx

# Healthchecks
docker run --health-cmd="curl -f http://localhost || exit 1" nginx

# Políticas de reinicio
docker run --restart=always nginx
docker run --restart=on-failure:3 nginx
```

### **Seguridad y Usuario**

```bash
# Ejecutar como usuario específico
docker run --user 1000:1000 nginx
docker run --user $(id -u):$(id -g) nginx

# Modo solo lectura
docker run --read-only nginx

# Capabilities
docker run --cap-drop ALL --cap-add NET_ADMIN nginx
```

---

## 🧹 **COMANDOS DE LIMPIEZA**

### **Limpieza Selectiva**

```bash
# Por componente
docker container prune         # Contenedores parados
docker image prune            # Imágenes dangling
docker image prune -a         # Imágenes no utilizadas
docker volume prune           # Volúmenes no utilizados
docker network prune          # Redes no utilizadas
docker builder prune          # Cache de build
```

### **Limpieza Total**

```bash
# Limpieza completa
docker system prune -a --volumes

# Con confirmación automática
docker system prune -a --volumes -f

# Limpieza por fecha
docker image prune --filter "until=24h"
docker container prune --filter "until=72h"
```

---

## 🔍 **COMANDOS DE DIAGNÓSTICO**

```bash
# Información detallada
docker version                # Versión cliente/servidor
docker system info           # Info completa del sistema

# Inspección profunda
docker inspect objeto_id      # Información JSON completa
docker diff contenedor_id    # Cambios en filesystem

# Debugging
docker run --rm -it imagen_id sh  # Contenedor temporal para debug
docker exec -it contenedor_id ps aux  # Procesos dentro del contenedor

# Exportar/Importar
docker save -o imagen.tar imagen:tag     # Exportar imagen
docker load -i imagen.tar               # Importar imagen
docker export contenedor_id > backup.tar  # Exportar contenedor
```

---

## 💡 **COMANDOS COMBINADOS ÚTILES**

```bash
# Parar y eliminar todos los contenedores
docker stop $(docker ps -q) && docker rm $(docker ps -aq)

# Eliminar imágenes sin tag
docker rmi $(docker images -f "dangling=true" -q)

# Ver solo IPs de contenedores
docker inspect $(docker ps -q) | grep IPAddress

# Logs de todos los contenedores
docker ps -q | xargs -I {} docker logs {}

# Backup de volumen
docker run --rm -v volumen_nombre:/data -v $(pwd):/backup ubuntu tar czf /backup/backup.tar.gz /data
```

---

## 📚 **ALIAS ÚTILES**

Agrega a tu `~/.bashrc`:

```bash
alias dps='docker ps'
alias dpsa='docker ps -a'
alias di='docker images'
alias dex='docker exec -it'
alias dlogs='docker logs -f'
alias dclean='docker system prune -a --volumes -f'
alias dstop='docker stop $(docker ps -q)'
alias drm='docker rm $(docker ps -aq)'
```