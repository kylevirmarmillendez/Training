# Docker Compose in the Real World

## Creating Compose File

`docker-compose.yml` 1 command and you're done

```code
version: '3'

services:
  redis:
    image: 'redist:3.2-alpine'
    ports:
      - '6379:6379'
    volumes:
      - 'redis:/data'

  web:
    build: '.'
    depends_on:
      - 'redis'
    env_file:
      - '.env'
    # environment:
      # FLASK_DEBUG: 'true'
    # image: 'username/name:1.0'
    ports:
      - '5000:5000'
    volumes:
      - '.:/app'

volumes:
  redis: {}
```
- `docker-compose.yml` configuration

## Docker Compose Commands

```code
docker compose --help 
``` 
- it will show the docker compose help

<br>

```code
docker compose build
``` 
- It will build images

<br>

```code
docker compose pull
``` 
- pulls the all the images in the docker hub

<br>

```code
docker compose up
```
- starting all containers

<br>


```code docker compose stop
```
- stopping all containers

<br>

```code
docker compose up --build -d
```
- build and run in the background and run containers so that you can use the terminal with other commands.

<br>

```code
docker compose logs -f
``` 
- Logs output display

<br>

```code
docker compose restart
``` 
- restarting all containers

<br>

```code
docker compose restart name1
``` 
- restarting one particular container

<br>

```code
docker compose exec name1
```
-  performing a command on a particular container
<br>


```code 
docker compose run name1 [[command] args]
``` 
- performing a command and exit after
<br>


```code
docker compose up name1
``` 
- Starts only name1 container, unless there is a depends_on option on docker-compose.yml

<br>


```code
docker compose rm
``` 
- deleting all stopped containers