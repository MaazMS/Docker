## Run - start a container  
1. docker run command is used to run docker container from an image. 
1. If image is not exists on the host it go out to dockerhub and pull the image down, but it only down first time.  

## Run - start a container exception
1. `$ docker run ubuntu` it runs an instance of ubuntu and exit immediately.    
1.  if ` $ docker ps -a ` it show status `Exited`  
1. Because unlike VM container are not meant to host os.  
1. Container are meant to run a specific task or process such as to host an instance of web server or application server or database.  
simply carry some kind of computation or analysis task.  
1. Once task is complete container exist.   
1. A container is only live as long as the process inside it is a live.  
1. if the web server inside the container is stopped or crash then container is an exit.  
1. There for an ubuntu is stop immediately it is base image there is no process or application running it default.  
1. if image is running any service and in this case you could instruct a docker to run a process with `docker run ubuntu sleep 5 `   
1. after 5 second container is stop,


## ps - list container  
1. ` $docker ps`  
1. list all the running container and some basic information such as container id, image, time, status,port,name.  

## ps -a - list of all container and previous run container 
1. list of all container and previous run container 

## Stop container 
1. docker stop provide by container id and image name.  
1. `$ docker stop image_name or container_id`   

## rm - Remove container   
1. `docker rm image_name or container_id`   
1. To remove stop or exited container permanently.    

## List of images   
1. List of images present in host machine.  
1. `$ docker images`   

## remove images  
1. Remove an image that you no longer.  
1. `$ docker rmi image_name`  
1. Remember you must ensure that no container are running of that image.  
1. you must stop and delete all dependent containers to be able to delete an image.  

## pull docker image   
1. It pull docker image.  
1. docker run command pull image and run image, but docker pull only pull docker image.  
1. `$ docker pull imager_name`   
1. Store image on a host.   

## Exec     execute command  
1. `$ docker run ubunu sleep 100`  
1. if see contain file inside the container.  
1. docker exec name_of_image cat /etc/hosts   

## Run - attach and detach   
1. doker run kodekloud/simple-webapp 
1. docker run -d kodekloud/simple-webapp  
1. docker attach name_of_image_or_container_id   
1. provide container id provide few character   


## Run image with version   
1. `$ docker run redis:4.0`  
1. image_name:version    
1. pull docker image with specific version  
1. After a colon is called `tag`   
1. if tag is not provide by image version it download the latest image.   


## RUN STDIN  
1. when the application is run in a docker it prints hello world.  
1. because by default the docker container does not listen to standard input even through you are attached to its console  
it is not able to read any input from you it doesn't have terminal to read input from it run non-interactive mode.
1. if you like to provide an interactive mode you must map to standard input of your host to docker container using `-i` parameter.    
1. `$ docker run -i app_name ` it show an app terminal input not interact with container terminal.
1. but still it not interact with container terminal provide `t` as parameter.   
1. `$ docker run -it app_name `   

## RUN PORT mapping/ port publishing   
1. run web application on docker host. when we run containerized application we see server is running.  
1. But how user access my application.  
1. There are two option. 
1. first use IP of docker container. every docker container assign IP by default, and it is access within docker host.
   1. open browser within docker host and `http://ip:port`    
   1. outside docker host we can not access it.   
1. second use IP of docker host and map port inside docker container to a free port on docker host.  
    1. To map port docker container port to localhost port using `-p` parameter. 
    1. `docker run -p 80:5000  kodekloud/webapp`  
    1. here port 80 is localhost port and port 5000 is docker container port.  
    1. We can not map to same port on docker host more than once.   
    
## RUN - Volume mapping
1. How data persistence on docker
1. Docker has its own isolated file system.  
1. if container is remove and stop all data is loss in file system.  
1. `docker stop image_name` and `docker rm image_name`   
1. if you want to persistence the data then map a directory outside the container on docker host to a directory inside the  
   container .  
1. docker container mysql data store on `/var/lib/mysql` to docker host `/opt/datadir` using `-v` parameter.    
1. `docker run -v /opt/datadir:/var/lib/mysql mysql`.   

## container full information  
1. `docker ps ` show information of docker information.   
1.  `docker inspect image_name`   

## how to check docker logs  
1. docker logs image_name    

## ENV variable in docker  
1. set environment variable
1. `docker run -e variable=vaalue image_name`     
1. multiple environment variable.   
1. `docker run -e variable=vaalue  variable=vaalue variable=vaalue image_name`    


