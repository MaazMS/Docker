## Run - start a container  
1. docker run command is used to run docker continer from an image. 
1. If image is not exists on the host it go out to dockerhub and pull the image down but it only down first time.  

## Run - start a container exception
1. `$ docker run ubuntu` it runs an instance of ubuntu and exit immediately.    
1.  if ` $ docker ps -a ` it show status `Exited`  
1. Because unlike VM container are not meant to host os.  
1. Container are meant to run specific task or procss such as to host an instance of web server or application server or database.  
simply carry some kind of coputation or analysis task.  
1. Once task is complete conatiner exist.   
1. A container is only live as long as the process inside it is a live.  
1. if the web server inside the container is stoped or crash then conater is exit.  
1. There for ubuntu is stop immediately it is base image there is no process or applicaation running it default.  
1. if image is running any service and in this case you could instruct docker to run a process with `docker run ubuntu sleep 5 `   
1. ifter 5 second container is stop,


## ps - list container  
1. ` $docker ps`  
1. list all the running conatiner and some basic information such as conainer id, image, time, status,port,name.  

## ps -a - list of all container and previous run container 
1. list of all container and previous run container 

## Stop conatiner 
1. docker stop provide by container id and image name.  
1. `$ docker stop image_name or container_id`   

## rm - Remove conatainer   
1. `docker rm image_name or container_id`   
1. To remove stop or exited container permanently.    

## List of images   
1. List of images present in host machine.  
1. `$ docker images`   

## remove images  
1. Remove an image that you no longer.  
1. `$ docker rmi image_name`  
1. Remember you must insure that no container are running of that image.  
1. you must stop and delete all dependent containers to able to delete an image.  

## pull docker image   
1. It pull docker image.  
1. docker run command pull image and run image, but docker pull only pull docker image.  
1. `$ docker pull imager_name`   
1. Store image on host.   

## Exec     execute command  
1. `$ docker run ubunu sleep 100`  
1. if see contain file inside the container.  
1. docker exec name_of_image cat /etc/hosts   

## Run - attach and detach   
1. doker run kodekloud/simple-webapp 
1. docker run -d kodekloud/simple-webapp  
1. docker attach name_of_image_or_container_id   
1. provide container id provide few character   
