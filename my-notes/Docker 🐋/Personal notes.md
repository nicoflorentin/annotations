### Comandos

Crea un contenedor **NUEVO** (vacío, sin tus datos)
`docker run`
Accede a un contenedor **EXISTENTE** (con tus datos reales)
`docker exec`
Ver imágenes
`docker images`
Ver contenedores
`docker ps -a`
Ver volúmenes
`docker volume ls`
Ver donde estan los datos del volumen
`docker volume inspect <name>
Inspeccionar
`docker inspect <id>`
Ver imágenes
`docker images`
Ver logs
`docker logs database`
Ver logs en tiempo real
`docker logs database -f`

### Comandos de emergencia
```bash
# Reiniciar la base
docker restart database

# Ver consumo de recursos
docker stats database
```

### Variables de entorno críticas
```bash
POSTGRES_PASSWORD=  # SIEMPRE configurar
POSTGRES_DB=        # Nombre de tu base
POSTGRES_USER=      # Usuario (default: postgres)
```

### Entrar a un contenedor de postgresql
```bash
psql -U $POSTGRES_USER -d $POSTGRES_DB
```

### Entrar a contenedor con mysql
```bash
docker exec -it mysql-db mysql -uroot -pmypassword
```

### Entrar a contenedor mariadb
```
mariadb -h 127.0.0.1 -P 3306 -u root -p
```
Ver bases de datos
```
SHOW DATABASES;
```
Usar tu base de datos
```
USE nocountry;
```
Ver tablas
```
SHOW TABLES;
```
Ver estructura de una tabla
```
DESCRIBE doctors;
```
Ver datos
```
SELECT * FROM doctors;
```
Salir
```
EXIT;
```