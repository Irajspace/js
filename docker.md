![alt text](image.png)
## what is the another alternative for docker
```
using virutalisation - create a virutal machine and share with my developers
- these are very expensive , they are overkill , we want to run only code we dont need virtualisation
why docker remains inexpensive
- it uses our kernal to run different containers can be linux , windows anything, it dont posess fully blown operarting system whereas in virutalation it contains full os


```
## docker container vs image
![alt text](image-1.png)
```
containers are isolated environments to run the docker images
when i write docker run -it ubuntu
means it has created a conatiner
you can run again on terminal
it will create again a container both their base files will be same but both containers can handle images independenlty
Docker Container

A running instance of an image.
Docker Container

A running instance of an image.
Has its own filesystem, processes, network, etc.
Can be started, stopped, and deleted.

Example:

docker run nginx

This creates and runs a container from the nginx image.
Analogy
Image = Class in OOP
Container = Object/Instance created from that class


```
![alt text](image-2.png)
![alt text](image-3.png)
![alt text](image-4.png)
## CLI commands
```
1)type docker and execute it will give help command means all the commands
2)docker ps -to list all containers(which are running)
3)docker ps --help- means you can run help it will show all the commands associated with it
4)docker ps --all-> all containers 
5)you can see aliases means it gives same functionality docker ps ,docker ls
6) docker run -it ubuntu->
    a) here run means create a container for an image
    b)it keeps the docker container attached it will not throw u back to ur machine, std input u can give commands
7) docker pull ubunutu- it will create image only nothine else
    a) then u run docker run -it ubunut - it will create new container for that image with some id
    b) then u run again docker run -it ubunut- it will create a new container again for that image with different it
8) to remove images first u have to remove the container associated with it then images
9)docker run -it --name my-container ubuntu to give container name

```
## Dockerize a node server
```
1) first create a Dockerfile(it is config file)
# base image
FROM ubuntu

# install node js 
{see from docs how to install node js in ubuntu
and type RUN (commands)}

# copy the source code to docker image
COPY index.js index.js{copy from source to destination}you can write anything COPY index.js and paste it into home/index.js
COPY package-lock.json package-lock.json
COPY package.json package.json

WORKDIR /home/app

RUN npm install




then build the image
docker built -t myapp .



```
![alt text](image-5.png)
![alt text](image-6.png)
## optimising build-layers
```
1) dont write FROM ubuntu - it contains useless things to run node you can search on dockerhub and get specific images for node js which can be alpine
2) add CMD ["npm" "start"]means it will run automatically on running the container



```
![alt text](image-7.png)
## port-mappings
```
docker run it -p 8000:8000 my-app the 2nd 8000 is inside container and 8000 in my machine
```
![alt text](image-8.png)
![alt text](image-9.png)

## more cli flags
```
 automatic port mappings
 EXPOSE PORT 8000
 docker run -it P my-app
 {then it will allocate random port meaning random:8000
 }

 to automatically kill a container when you are not running
 docker run -it -P --rm my-app
```
## publish our custom-image in dockerhub
```
1) create a repository
2)to post it you have to same name of docker image as your in hub.docker.com
you can do this by buiding with that name
3) then push that image
4)2nd way is docker tag my-app rishiraj/nodejs
```

## multi-stage-builds
![alt text](image-10.png)
![alt text](image-11.png)
![alt text](image-12.png)
![alt text](image-13.png)
![alt text](image-14.png)
```
1) once build is done why we need src file
2)you are first building then copying the build folder to your runner
3)to specify the dockerfile which you want to run use -f
4)it copies the file and deletes the 1st stage


```
## secure management
![alt text](image-15.png)
![alt text](image-16.png)

## networking
![alt text](image-17.png)
![alt text](image-18.png)
![alt text](image-19.png)
```
when you pull busybox and u can ping googl.com so whose ip address and whose net it is using ??
- docker network ls these are all the commands
- it creates its own subnet
- you have to communicated between diff containsers using ip address
```
![alt text](image-20.png)
## how to create own bridge network
```
- docker network create milkyway
- to run any container in this particular network
 - docker run -itd --network=milkyway --rm --name=spiderman busybox

- on same network they can connect and on diff they cant
- to connect container of diff network to a diff network  use connect
- docker network connect milkyway container_two
```
## how to use different networks
![alt text](image-21.png)
![alt text](image-22.png)


## docker volumes
![alt text](image-23.png)
![alt text](image-24.png)
![alt text](image-26.png)
```
so whats are u doing here is you want to create a reference (link)of your folders in your docker container means wherenver docker container gets deleted its changes will be alived since its originally in host computer

```
## how to write multiple commands
![alt text](image-25.png)


## custom docker volumes
![alt text](image-27.png)
```
type docker volume
to create docker volume create custom_data

```
## docker compose
```


```