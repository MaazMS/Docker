## docker engine   
1. When you install a docker it installs some component.  
1. component installation with a docker.  
    1. Docker CLI (command line interface)  
    1. REST API server
    1. Docker Deamon  
    
## Docker Deamon 
1. Docker Deamon is a background process that manage docker object such as image, container, networks, volumes, 

## REST API server  
1. docker REST API server is the API interface that program can use to talk with a docker deamon and provide instruction.  
1. It is also used to create your own resource using REST API.  

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
1. docker use namespace to isolate workspace process such as ProcessID, Network, unix Timesharing, Mount, InterProcess,  
1. These are created their own namespace there by providing isolation between containers.     

## Technique of namespace of isolation  
1. Process ID namespaces  
1. when ever linux system is boots up it start with jus one process and process id.  
1. This is root process and kicks all the process in the system.  
1. Process id is unique and two process can not have same id.  
1. If we create a container which is basically child system process within current system needs to think that it is independent  
system on its own and it has its own set of processes originating from a root process with a process id.  
![]()     
1. But there is no hard isolation between container and underline host os.  
1. There for the process id of container and underline host os and same process id. there for we use namespace two give unique   
process id.  
1. Using namespace for process id, for example when the processes start within contianer it's actually just another set of processes  
on the base host os, and it gets the next available process id in this case 5 and 6.    
![]()  
   
## Cgroups  
1. docker host and conatiener share the same system resources such as CPU, memory.  
1. How much resources are dedicated to host os and container.  
1. Hoe does docker manager and share resources between the conatinaner.   
1. There is no restriction as to how much of resources a container can use.  
1. But there is a way to restrict the resources for container.   
1. Docker use `cgroup`  or `control group` it is use to restrict the resources.  
1. It is also allocate the fix amount for resources for each container.  
1. `$ docker run --cpu=.5 ubuntu` contianer does not take more then 50% of cpu.  
1.  `$ docker run --memory=100m ubuntu` contianer use 100MB memory.    

    