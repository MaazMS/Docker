## docker engine   
1. When you install docker it install some component.  
1. component install with docker.  
    1. Docker CLI (command line interface)  
    1. REST API server
    1. Docker Deamon  
    
## Docker Deamon 
1. Docker Deamon is a background process that manage docker object such as image, container, networks, volumes, 

## REST API server  
1. docker REST API server is the API interface that program can use to talk with a docker deamon and provide instruction.  
1. It is also use to create your own resource using REST API.  

## Docker CLI  
1. Docker CLI  is nothing but command line interface.  
1. It is use such as run container, stop container etc.  
1. It uses The REST API to interact with a docker deamon.  
1. Docker CLI need not necessarily be on the same host.    
1. It could be on another system like, a laptop and can still work with a remote work engine. 
1. remote docker engine 
    1. `$ docker -H=remote-docker-engine:port `  
    1. run image `$ docker -H=10.123.2.1.2375 run nginx`  
    
## containerization  
1. docker use namespace to isolate workspace process such as ProcessID, Netwrok, unix Timesharing, Mount, InterProcess,  
1. These are create their own namespace there by providing isolation between containers.   

    