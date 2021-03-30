## docker registry 
1. It is a central repository of all docker image.  
1. `docker run nginx`  
1. It runs instance of nginx image.  

* Explain 
    1. Here `nginx` is the image name or repository name in dockerhub.    
    1. image `nginx/nginx` user account name / repository name.  
    1. image : docker.io/nginx/nginx   
    
## private registry 
1. It is used by organization or personal use.  
1. To use private registry images. 
    1. login private registry  
    1. `$ docker login private-registry.io`  
    1. username and password enter.  
1. Before pulling image private registry login private registry.  
1. deploy private registry.  
    1. `$ docker run -d -p 5000:5000 --name image_name  image_name:2`   
1. image private registry.  
    1. `$ docker image tag image_name localhost:5000 image_name`  
    1. `$ docker push localhost:5000 image_name`
    1. `$ docker pull localhost:5000 image_name`
    