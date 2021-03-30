## Storage 
1. when install docker on system it create file system.  
``` 
/var/lib/docker
    /aufs 
    /containers 
    /images 
    /volumes
``` 
1. container folder: 
    1. All files related to container are store in container file.   
1. images folder:     
    1. All files related to images are store in images file.  
1.  volumes folder: 
   1. All volumes created to are store in volumes file.    

## How docker store the file of the image and container
1. To understand How docker store the file of the image and container we need to understand `layered architecture`  
### layered architecture 
1. when docker build image it builds these in layered architecture.
1. Each line of instruction is one layered in docker image with just change from a previous layer with size.
1. you can see all layered follow `docker hostory user_name/image_name`  
**Advantage** 
   1. The advantage of layered architecture is that  
   1. Let example two same application but different docker file, same base os,python package and dependency and different source code ,entry point. 
   1. When build the image same os ubuntu, python package and dependency then docker is not build first three layer, 
      1. layer one base ubuntu  
      1. layer two changes in apt packages 
      1. layer three changes in apt packages 
   1. It reuses same three layered for previous application from a cache.  
   1. It creates last two layered one is source code and second is entry point.  
   1. This way docker build images faster and efficiently and save disk space. 
   1. It is applicable for an update source code as well as.  
   1. If update the any docker image layer docker is simple reuses all the perilous layer from a cache and quickly rebuild   
      application with the latest source code. 
   1. save time.  
   
##  layered architecture next step 
1. All the image layered are created when we run docker build command.  
1. We got docker image.     
1. once the docker is build the image form image layered we can not modify an image layered, and so they are `read-only`  
1. we can only modify them by initiating new build. 
1. when you run container based on this docker image, docker create a container based of this layers and creates a new `writeble`   
layer on top of the image layer.  
1. The `read write`layer is used to store data created by the container.  
1. The life of `read write`layer is only container is live when container is destory this layere is remove and all data is loss.  
1. Remember this same image is shared by all container created using this image.  
1. How to change the source code ??  
   1. The image layer is read only mode, there for we can not modify it.  
   1. The image later is share to all container which is read by using this image.  
   1. But I can still modify source code. 
      1. But save  modify source code file docker automatically create copy of the file in `read write` layer.  
      1. This is called `Copy on write ` mechanism.  

## Persistent volume 
1. When build the docker image and run the container it creates read write layer. 
1. we create the file and read write layer. but if the container is deleted the data is loss. 
1. There for we create persistent volume.  
1. It saves data after delete container.  
1. There are two types of volume. 
   1. volume mounting (volume mounting mount volume from volume directory) 
   1. bind mounting (bind mounting mount a directory from any location on docker host) 
1. First we create volume `docker volume create volume_name`  
1. It creates folder inside `var/lib/volume/` and folder name `volume_name`.    
1. When we run docker container we mount the volume i.e `docker run -v volume_name:var/lib/volume/volume_name image_name`  
1. What happen when we can not create volume and run docker with volume,? 
   1. docker is automatically create volume and mount to container.  
1. what happen when aur data is already in another location inside docker host and store aur data on that location.  
   1. We run container docker run -v complete_path_folder(we would to mount). 
   1. `docker run -v /data/mysql:var/lib/mysql mysql`   
   1. This is called bind mounting.   
   
1. This is new command for volume,
```bash

$  docker run --mount type=bind,source=/data/mysql,target=var/lib/mysql mysql
```  
   
## All this responsible by storage driver.  
1. It enables layered architecture, 
1. The selection of storage driver based on os. 
1. Docker will choose the best driver based on os. 
1. ubuntu use `AUFS` storage driver.  

   
   