https://www.youtube.com/watch?v=GFgJkfScVNU&ab_channel=JavaScriptMastery

**Advantages :** 
- Consistency across environments
- Isolation
- Portability
- Faster virtuall machine
- Scalability
- DevOps integration

**How it works ?**

Images:
Includes de code, runtimes, libraries, operating system, system tools.

Containers:
Runnable instance of a docker image, we can run multiple containers from a simple image. It's like a wine runner (config) and wine prefix (instance).

Docker network:
Communication channel between containers or external services mantaining isolation.

**Docker workflow:**

Docker client:
Interface to interacting with docker, command line or graphical interface

Docker host - Docker daemon:
Background process to manage containers on the host system. Listen for docker clients commands, create images, build images, etc.

Docker registry - Docker hub:
Centralized repository of docker images, hosts public and private registries or packages

![[Pasted image 20250516020841.png]]

13:47
**DOCKERFILE**
Starts from dockerfile and tells how to build an imagen for the application, specifics instructions and keywords

### **Commands**

WORKDIR - COPY - RUN - EXPOSE - ENV - ARG - VOLUME - CMD - ENTRYPOINT

**Run a container**
```bash
"-it para INTERACTIVO"
docker run -it ubuntu
```

**Create docker images**
./Dockerfile
```
FROM node:20-alpine

WORKDIR /app

COPY . .

CMD node hello.js
```


```bash
docker build -t hello-docker .
```

```bash
"show images"
docker images
```

```bash
"open app in shell mode"
docker run -it hello-docker sh
```

**React docker application**
```dockerfile
# set the base image to create the image for react app
FROM node:20-alpine

# create a user with permissions to run the app
# -S -> create a system user
# -G -> add the user to a group
# This is done to avoid running the app as root
# If the app is run as root, any vulnerability in the app can be exploited to gain access to the host system
# It's a good practice to run the app as a non-root user
RUN addgroup app && adduser -S -G app app

# set the user to run the app
USER app

# set the working directory to /app
WORKDIR /app

# copy package.json and package-lock.json to the working directory
# This is done before copying the rest of the files to take advantage of Docker’s cache
# If the package.json and package-lock.json files haven’t changed, Docker will use the cached dependencies
COPY package*.json ./

# sometimes the ownership of the files in the working directory is changed to root
# and thus the app can't access the files and throws an error -> EACCES: permission denied
# to avoid this, change the ownership of the files to the root user
USER root

# change the ownership of the /app directory to the app user
# chown -R <user>:<group> <directory>
# chown command changes the user and/or group ownership of for given file.
RUN chown -R app:app .

# change the user back to the app user
USER app

# install dependencies
RUN npm install

# copy the rest of the files to the working directory
COPY . .

# expose port 5173 to tell Docker that the container listens on the specified network ports at runtime
# To access it from the host, you need to use "port mapping" (-p).
# Important: if the app inside the container only listens on "localhost", it will be trapped inside the container.
# "-p 5173:5173" maps port 5173 of the host to port 5173 of the container.
# This makes the app accessible from your host machine at http://localhost:5173
# docker run -p 5173:5173 react-docker
EXPOSE 5173

# command to run the app
CMD npm run dev

```

**.dockerignore**
```txt
node_modules/
```

**Port mapping**
```bash
docker run -p 5173:5173 react-docker
```

**PS**
```bash
# show active docker containers 
docker ps

# show all docker containers (active/inactive)
docker ps -a
```

**Stop a container**
```bash
docker stop <container-id>
```

**Prune**
```bash
# remove all stopped containers
docker container prune

# remove a specific container
docker rm <id> || <name> # to stop running containers use --force param
```

**Listen to file changes**
```bash
# -v (volume) creates a volume that keep track of all of the changes
docker run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules react-docker
```

Login and publish an image
```bash
docker login
docker tag react-docker <username>/<name_of_image>
docker push <username>/<name_of_image>
```


44:30
### Docker Compose

uses yaml file to configure the services, networks and volumes
multiple orchestrated containers interacting via nodes

Initiate docker compose project
```bash
docker init
```

Important files
- Dockerfile
- dockerignore
- compose.yaml

**compose.yaml**
![[Pasted image 20250830175439.png]]
**up**
```bash
sudo docker compose up
```

**docker compose watch**
listen to our changes and does some action : 
- sync files when moved from the host to the container
- rebuild
- sync-restart : merges the sync and rebuild process

```yaml
# specify the version of docker-compose
version: "3.8"

# define the services/containers to be run
services:
  # define the frontend service
  # we can use any name for the service. A standard naming convention is to use "web" for the frontend
  web:
    # we use depends_on to specify that service depends on another service
    # in this case, we specify that the web depends on the api service
    # this means that the api service will be started before the web service
    depends_on: 
      - api
    # specify the build context for the web service
    # this is the directory where the Dockerfile for the web service is located
    build: ./frontend
    # specify the ports to expose for the web service
    # the first number is the port on the host machine
    # the second number is the port inside the container
    ports:
      - 5173:5173
    # specify the environment variables for the web service
    # these environment variables will be available inside the container
    environment:
      VITE_API_URL: http://localhost:8000

    # this is for docker compose watch mode
    # anything mentioned under develop will be watched for changes by docker compose watch and it will perform the action mentioned
    develop:
      # we specify the files to watch for changes
      watch:
        # it'll watch for changes in package.json and package-lock.json and rebuild the container if there are any changes
        - path: ./frontend/package.json
          action: rebuild
        - path: ./frontend/package-lock.json
          action: rebuild
        # it'll watch for changes in the frontend directory and sync the changes with the container real time
        - path: ./frontend
          target: /app
          action: sync

  # define the api service/container
  api: 
    # api service depends on the db service so the db service will be started before the api service
    depends_on: 
      - db

    # specify the build context for the api service
    build: ./backend
    
    # specify the ports to expose for the api service
    # the first number is the port on the host machine
    # the second number is the port inside the container
    ports: 
      - 8000:8000

    # specify environment variables for the api service
    # for demo purposes, we're using a local mongodb instance
    environment: 
      DB_URL: mongodb://db/anime
    
    # establish docker compose watch mode for the api service
    develop:
      # specify the files to watch for changes
      watch:
        # it'll watch for changes in package.json and package-lock.json and rebuild the container and image if there are any changes
        - path: ./backend/package.json
          action: rebuild
        - path: ./backend/package-lock.json
          action: rebuild
        
        # it'll watch for changes in the backend directory and sync the changes with the container real time
        - path: ./backend
          target: /app
          action: sync

  # define the db service
  db:
    # specify the image to use for the db service from docker hub. If we have a custom image, we can specify that in this format
    # In the above two services, we're using the build context to build the image for the service from the Dockerfile so we specify the image as "build: ./frontend" or "build: ./backend".
    # but for the db service, we're using the image from docker hub so we specify the image as "image: mongo:latest"
    # you can find the image name and tag for mongodb from docker hub here: https://hub.docker.com/_/mongo
    image: mongo:latest

    # specify the ports to expose for the db service
    # generally, we do this in api service using mongodb atlas. But for demo purposes, we're using a local mongodb instance
    # usually, mongodb runs on port 27017. So we're exposing the port 27017 on the host machine and mapping it to the port 27017 inside the container
    ports:
      - 27017:27017

    # specify the volumes to mount for the db service
    # we're mounting the volume named "anime" inside the container at /data/db directory
    # this is done so that the data inside the mongodb container is persisted even if the container is stopped
    volumes:
      - anime:/data/db

# define the volumes to be used by the services
volumes:
  anime:
```

01:02:30

