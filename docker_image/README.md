1. why we need to create an image on a docker?    
   1. The application your developing will be derived for ease of shipping and development.  
    
## create docker image  
step 1: what are the step to deploy application manually in wright order.    
    1. FROM ubuntu 
    1. update apt repo  
    1. install dependency using apt  
    1. install python dependency using pip   
    1. copy source code to /opt folder  
    1. run web server using flask command 
step 2: create dockerfile and write all manual step like this  
    1. FROM Ubuntu  
    1. RUN apt-get update  
    1. RUN apt-get install python  
    1. RUN pip install flask  
    1. RUN pip install flask-mysql  
    1. COPY . opt/source-code  
    1. ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run  
step 3: build docker image  
    1. `$ docker build Dockerfile -t user_name/image_name`
    1. It create image locally. 
    1. To provide image public them push docker image to dockerhub.  
    1. `$ docker push user_name/image_name`  
    
## Dockerfile 
1. It is simple text file return in a specific format that docker can understand.    
1. It is an instruction and argument format.  
1. Every thing on left side is an instruction example `FROM`, `RUN`, `COPY`, `ENTRYPOINT` and all are capital latter.  
1. Each instruction performs a specific task.  
1. Every thing on right are argumrnt of the instruction. example ` apt-get update`, `ubuntu` etc.  
1. All docker file start from `FROM` instruction. in our example is ubuntu base image.  

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
## docker build  
1. To see all step and their result of docker file.  
1. `$ docker build . `  
1. if any step fail or add more step you wouldn't have to start all over again and again.  
1. just run command    
1. `$ docker build Dokcerfile -t user_name/image_name`