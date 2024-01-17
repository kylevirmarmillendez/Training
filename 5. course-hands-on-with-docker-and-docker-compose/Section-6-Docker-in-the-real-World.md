# Docker in the real world.

**Creating a Dockerfile**
```python
FROM python:3.9.18-alpine
```
- Setting up the alpine version of python repo.

```Docker
RUN mkdir /app
```
- making directory with linux
- it allows run any scripts.

```code
WORKDIR /app
```
- Pass in a directory path.


```code
COPY requirements.txt
```
- copy collects the source and the destination.

```CODE 
RUN  pip install -r requirements.txt
```
- installing the file dependencies.


```code
LABEL
```
- expects to you a key and a value
- it is optional

```php
CMD flask run --host=0.0.0.0 --port=5000
```
- Setting the server port in running the python application.
<br>

The instructions how to create a Dockerfile: 
```code
FROM python:2.7-alpine

RUN mkdir /app
WORKDIR /app

COPY requirements.txt requirements.txt
RUN  pip install -r requirements.txt

COPY . .

LABEL maintainer="Kyle Virmar Millendez <kylevirmarmillendez@gmail.com>"\
    Version="1.0"

CMD flask run --host=0.0.0.0 --port=5000
```


**Building a Docker Image**
```code
docker image build -t web1 .
```
- run this command
- make sure that you are using the latest docker alpine version. 

<br>

```code
docker image inspect web1
```
-  Gives you a json format with a lot of useful information about our image.

<br>

```code
docker image build -t web1:1.0 .
```
- This how to mag tag with the image.
- it like making your on version control.

<br>

```code
docker image rm web1:1.0
```
- to delete the docker image

<br>

```code
docker login
```
- to authenticate the cli to the docker hub.

<br>

```code
docker image tag web1 kvmillendez/web1:latest
```
- creating online version of your directory.

<br>

```code
docker image push kvmillendez/web1:latest
```
- This will push the image to the docker hub.

<br>

```code
docker image rm -f fda5
docker image rm web1:latest
```
- Deleting the image in the local server.

<br>

```code
docker container ls
```
- show all docker container inside an image.


```code
docker container run -it -p 8000:5000 -e FLASK_APP=app.py web1
```
- to run the docker app to the public network.

<br>

```code
docker container run -it --rm --name web1  -p 8000:5000 -e FLASK_APP=app.py web1
```
- you can do this instead, because this command will set the name of the container and it will automatically delete the container after stopping.

<br>

```code
docker container run -it --rm --name web1  -p 8000:5000 -e FLASK_APP=app.py -d web1
```
- the container is still running but you can use same terminal for new commands
<br>

```code
docker container run -it -p 8000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 web1
```
- Debug the code for changes in the docker file


```code
docker container run -it -p 8000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v %CD%:/app  web1
```
- where you can edit your file inside the app.py

<br>

```php
docker container exec -it -web1 bash
```
- allow linux command on windows

Its not working on my side.


<br>


## Docker Network

If the Docker file is running you can acces the application within the Local Area Network either Wired or Wireless.

`localhost:8000`