## Networking 
1. When you install a docker it creates three network automatically.   
    1. bridge it is default network.  
    1. non
    1. host  
    
1. To run docker on specific network then 
    1. docker run ubuntu it run on bridge network, it is private internal network and all container attach by default and range `172` series 
    1. docker run ubuntu --network= none, it run on a none network and not connect to outside on a container and other container. it run isolated network. 
    1. docker run ubuntu it run on bridge network.
    
1. Access container. 
    1. map the port. 
    1. container access on docker host port, but in docker host only one container is running no required port mapping.    
    
1. How to create islolated network. 
    1. All container is share same network bridge. 
    1. Create isolated network within a docker and connect the container to this network. 
    1. ` $ docker network create --drive bridge --subnet 182.18.0.0/16 custorm-isolated-network`  
    1. list all network `$ docker network ls`  
    1. see network setting `$ docker inspect image_name_or_container_id` network settring.
    
1. Embedded DNS 
    1. using internal IP but it is not sure that when system is reboot IP get changed.   
    1. mysql.connect(container_name).  
    1. Docker has built-in DNS server.  
    1. It resolves DNS using container name.   


## view list of network 
1. docker network ls 

    
## remove network 
1. docker network rm network_name   

## How to find-our running docker container network name 
1. docker inspect container_name | grep NetworkMode   

## How to override network name  
1. docker-compose -p network_name up -d   

## How to create network 
1. docker network create network_name 

## How to disconnect container from network 
1. docker network disconnect network_name container_name