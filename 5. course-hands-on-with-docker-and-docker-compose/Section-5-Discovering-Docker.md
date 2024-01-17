# Discovering Docker

### Hello World Docker.

```cli 
docker run hello-world
```
- Its going to perform  4 key steps.
    -   The Docker client contacted the Docker daemon.
    - The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
    - The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
    - The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

<br>

**Docker Image vs Container**
    

**Docker Image**
- is a combination fo a file system and parameters.
- No state and doesn't change
- You can download, build and run with it.
- One image has many container


**Docker Containers**
- Docker containers are immutable
- The changes will not be saved after  you stop the container.

<br>

**Docker HUB**
- is  a Docker Registry is the place for you to store your docker image.


**2 ways to Build a docker image**
- docker commit
- Dockerfile

