# Dockerfile is a text document without extends format file containing all the user requires to call command line to assemble image
**image vs container:**
- an image is the application we want to run 
- a container is an instance of the image we want to running as a process
- i can have many containers running off the same image
- docker's default image registry is docker hub
# what happens in docker container run 
1 look for that image locally in image cache, doesn't find anything
2 then looks in remote image repository (registry) by default it's docker hub
3 download latest version 
4 create new container based on that image and prepare to start
5 give it an vertual ip on private network inside docker engine
6 open up port 80 on host and forwards to port 80 in container
7 starts container by using the CMD in the image dockerfile

# Instruction arguments
## 1 FROM 
* FROM<image> [AS <name>]
* FROM <image>[:<tag>] [AS <name>]
* FROM <image>[@<digest>] [AS <name>]
### FROM is BASE image to build image and must-have argument in 1st line
Ex: FROM node:lts-alphile

## 2 RUN
* RUN <command>
* RUN ["executable", "param1", "param2"]
### RUN is linux command to execute when processing build 
Ex: RUN apt-get update 
    RUN apt-get install curl -y
  or shorten it:
    RUN apt-get update; \
        apt-get install curl -y

## 3 ADD 
* ADD [--chown=<user>:<group>] <src>... <dest>
* ADD [--chown=<user>:<group>] ["<src>",... "<dest>"]
### ADD do copy directories or folders from local machine or remote src to **file system of image** - *dest*
Ex: 
ADD hom* /mydir/
ADD hom?.txt /mydir/
ADD test.txt relativeDir/

## 4 COPY 
* COPY [--chown=<user>:<group>] <src>... <dest>*
* COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
### COPY is the same with ADD but cannot copy from remote src

## 5 ENV 
* ENV <key>=<value> ...
### ENV declare environment variables for the following arguments such as: 
- ADD
- COPY
- ENV
- EXPOSE
- FROM
- LABEL
- STOPSIGNAL
- USER
- VOLUME
- WORKDIR
Ex: ENV PORT=8080 USERNAME="cityhunter" PASSWORD="123456"

## 6 CMD
* CMD ["executable","param1","param2"]
* CMD ["param1","param2"] 
* CMD command param1 param2
### CMD is command to run after container start from image, can declare multiple but just run last CMD
Ex: FROM ubuntu
CMD echo Viblo

## 7: USER
* USER <user>[:<group>]
* USER <UID>[:<GID>]
### USER is used to set username or UID to use after run image and used for comand inside **RUN** **CMD** **ENPOINT**
## LABEL 
*LABEL <key>=<value> <key>=<value> ... <key>=<value>
### To declare meta data in image
Ex: LABEL version="2.0"

# Create image with Dockerfile
docker build -t <image-name> .


