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
Runnable instance of a docker image, we can run multiple containers from a simple image. It's like a wine runner and wine prefix.

Docker network:
Communication channel between containers or external services mantaining isolation.

**Docker workflow:**

Docker client:
Interface to interacting with docker, command line or graphical interface

Docker host - Docker daemon:
Background process to manage containers on the host system. Listen for docker clients commands, create images, build images, etc.

Docker registry - Docker hub:
- [ ] Centralized repository of docker images