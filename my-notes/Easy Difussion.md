
## 1. **Usar Docker (Recomendación Principal)**

La forma más limpia es usar Docker, ya que todo queda contenido:

```bash
# Instalar Docker si no lo tienes
sudo apt update
sudo apt install docker.io docker-compose
sudo usermod -aG docker $USER
# Reiniciar sesión después de este comando

# Ejecutar Easy Diffusion en Docker
docker run -it --rm \
  --gpus all \
  -p 9000:9000 \
  -v $(pwd)/easy-diffusion-data:/data \
  easydiffusion/easydiffusion
```

**Ventajas:**

- Cero impacto en el sistema host
- Desinstalación completa: `docker rmi easydiffusion/easydiffusion`
- Aislamiento total de dependencias

## 2. **Instalación en Directorio Contenido**

Basándome en los scripts que subiste, Easy Diffusion ya está diseñado para ser bastante autocontenido:

```bash
# Crear directorio específico
mkdir ~/easy-diffusion-install
cd ~/easy-diffusion-install

# Descargar e instalar
wget https://github.com/easydiffusion/easydiffusion/releases/latest/download/easy-diffusion-linux.zip
unzip easy-diffusion-linux.zip
chmod +x start.sh
./start.sh
```

## 3. **Usar un Entorno Virtual Python Aislado**

```bash
# Crear entorno virtual dedicado
python3 -m venv ~/easy-diffusion-venv
source ~/easy-diffusion-venv/bin/activate

# Instalar en directorio específico
mkdir ~/easy-diffusion-clean
cd ~/easy-diffusion-clean
# Continuar con la instalación normal
```

## 4. **Monitorear Cambios del Sistema**

Antes de instalar, puedes crear un snapshot de tu sistema:

```bash
# Crear lista de paquetes instalados ANTES
dpkg --get-selections > ~/pre-install-packages.txt
pip3 list > ~/pre-install-pip.txt

# Después de la instalación, comparar:
dpkg --get-selections > ~/post-install-packages.txt
pip3 list > ~/post-install-pip.txt
diff ~/pre-install-packages.txt ~/post-install-packages.txt
```

## 5. **Script de Desinstalación Limpia**

Crea este script para desinstalar completamente:

```bash
#!/bin/bash
# desinstalar-easy-diffusion.sh

echo "Desinstalando Easy Diffusion..."

# Eliminar directorio principal
rm -rf ~/easy-diffusion-install

# Eliminar entorno conda/mamba creado por Easy Diffusion
rm -rf ~/easy-diffusion-install/installer_files

# Limpiar variables de entorno (agregar a ~/.bashrc si se modificó)
unset PYTHONNOUSERSITE
unset PYTHONPATH

# Eliminar cualquier servicio o proceso relacionado
pkill -f "easy.*diffusion"

echo "Desinstalación completa"
```

## **Mi Recomendación Final:**

1. **Usa Docker** si tu GPU es compatible y tienes experiencia básica con contenedores
2. **Si no usas Docker**, instala en un directorio dedicado (`~/easy-diffusion`) y evita usar `sudo` durante la instalación
3. **Mantén un registro** de lo que se instala para poder revertirlo

## **Verificación de Limpieza:**

Después de la instalación, verifica que no se hayan modificado archivos del sistema:

```bash
# Verificar que no se instalaron paquetes de sistema
sudo find /usr -name "*diffusion*" -o -name "*stable*"

# Verificar modificaciones en PATH
echo $PATH | tr ':' '\n' | grep -i diffusion
```

El script `bootstrap.sh` que subiste muestra que Easy Diffusion usa micromamba y se instala de forma bastante autocontenida en `installer_files/`, lo cual es buena señal para una desinstalación limpia.




# Instalar y correr
Te explico paso a paso cómo instalar y ejecutar Easy Diffusion con Docker en Ubuntu:

## 1. **Instalar Docker**

```bash
# Actualizar el sistema
sudo apt update

# Instalar dependencias necesarias
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Agregar la clave GPG oficial de Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Agregar el repositorio de Docker
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Actualizar la lista de paquetes
sudo apt update

# Instalar Docker
sudo apt install docker-ce docker-ce-cli containerd.io

# Verificar que Docker esté funcionando
sudo docker --version
```

## 2. **Configurar Docker para tu usuario**

```bash
# Agregar tu usuario al grupo docker (para no usar sudo)
sudo usermod -aG docker $USER

# Aplicar los cambios (necesitas cerrar y abrir sesión o reiniciar)
newgrp docker

# Verificar que funciona sin sudo
docker --version
```

## 3. **Instalar NVIDIA Container Toolkit (para GPUs NVIDIA)**

Si tienes una GPU NVIDIA:

```bash
# Configurar el repositorio
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

# Instalar nvidia-container-toolkit
sudo apt update
sudo apt install nvidia-container-toolkit

# Reiniciar Docker
sudo systemctl restart docker

# Verificar que funciona
docker run --rm --gpus all nvidia/cuda:11.0.3-base-ubuntu20.04 nvidia-smi
```

## 4. **Crear estructura de directorios**

```bash
# Crear directorio para datos persistentes
mkdir -p ~/easy-diffusion-docker/{models,outputs,config}
cd ~/easy-diffusion-docker

# Crear directorio para modelos (opcional, para organizarse mejor)
mkdir -p models/{stable-diffusion,vae,controlnet,lora}
```

## 5. **Ejecutar Easy Diffusion con Docker**

### Opción A: Comando directo (recomendado para empezar)

```bash
docker run -it --rm \
  --name easy-diffusion \
  --gpus all \
  -p 9000:9000 \
  -v ~/easy-diffusion-docker/outputs:/app/outputs \
  -v ~/easy-diffusion-docker/models:/app/models \
  easydiffusion/easydiffusion:latest
```

### Opción B: Con docker-compose (más profesional)

Crea un archivo `docker-compose.yml`:Luego ejecuta:

```bash
# Instalar docker-compose si no lo tienes
sudo apt install docker-compose

# Ejecutar
docker-compose up -d

# Ver logs
docker-compose logs -f

# Detener
docker-compose down
```

## 6. **Acceder a Easy Diffusion**

Una vez que el contenedor esté ejecutándose:

1. Abre tu navegador
2. Ve a: `http://localhost:9000`
3. ¡Listo! Ya puedes usar Easy Diffusion

## 7. **Comandos útiles de Docker**

```bash
# Ver contenedores en ejecución
docker ps

# Ver logs del contenedor
docker logs easy-diffusion

# Entrar al contenedor (para debugging)
docker exec -it easy-diffusion bash

# Detener el contenedor
docker stop easy-diffusion

# Eliminar el contenedor
docker rm easy-diffusion

# Ver imágenes descargadas
docker images

# Eliminar la imagen (desinstalación completa)
docker rmi easydiffusion/easydiffusion:latest
```

## 8. **Script de inicio rápido**

Crea un script para facilitar el uso:```bash

# Hacer el script ejecutable

chmod +x easy-diffusion.sh

# Usar el script

./easy-diffusion.sh start # Iniciar ./easy-diffusion.sh status # Ver estado ./easy-diffusion.sh stop # Detener ./easy-diffusion.sh uninstall # Desinstalar completamente

````

## **Ventajas de esta instalación:**

✅ **Completamente aislada** del sistema  
✅ **Fácil de desinstalar** (solo eliminar la imagen Docker)  
✅ **Sin conflictos** con otras instalaciones de Python  
✅ **Datos persistentes** en directorios específicos  
✅ **Fácil de actualizar** con `docker pull`  

## **Desinstalación completa:**

```bash
# Detener y eliminar contenedor
docker stop easy-diffusion
docker rm easy-diffusion

# Eliminar imagen
docker rmi easydiffusion/easydiffusion:latest

# Eliminar datos (opcional)
rm -rf ~/easy-diffusion-docker
````

¡Con esto tendrás Easy Diffusion funcionando de forma completamente limpia y aislada!