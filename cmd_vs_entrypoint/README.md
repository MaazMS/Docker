## command , argument and entrypoint 

## scenario 1  
1. `$ docker run ubuntu` it runs an instance of ubuntu and exit immediately.  
1. `$ docker ps ` it not shows docker image.       
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

* you can see ubuntu, mysqld ,nginx image last line means CMD[].  
1. ubuntu image `CMD["bash"]` bash is default command for ubuntu image.  
1. Now bash is not a process like web server and database it is shell that listen input from terminal if it not find termianal it exist. 

* solution 1
1. append the command it overrides the default command specified in the image.   
1. ` $ docker run ubuntu sleep 5`  
1. it run sleep program to 5 second and then exist.  

* solution 2 
1. how to make that change permanently.  
1. It mean when you run image it always run sleep command when it start.  
1. you create your own image from base ubuntu and specify a new command. 
```bash
FROM ubuntu 
CMD sleep 5
``` 
1. There are different way to write CMD, 
   1. CMD command parameter i.e CMD sleep 5 
   1. CMD ["command",  "parameter"]  i.e CMD ["sleep", "5"]
   1. 
1. `$ docker build -t ubuntu-sleeper` 
1. ` $ docker run ubuntu-sleeper`   

* solution 3  
1. How to give sleep point different each time, because in CMD we hardcode the sleep time.  
1. Then use `ENTRYPOINT`.  
```bash
FROM ubuntu 
ENTRYPOINT ["sleep"]
```    
1. ENTRYPOINT : It is the command instruction you can specify a program it run when container start.  
1. if you enter 20 it appends 20 second to sleep parameter `$ docker run ubuntu-sleeper 20 `    
1. when not specify time `$ docker run ubuntu-sleeper` it show error `sleep missing operand`    

## how to define default time and dynamic time
1. use both `ENTRYPOINT` and `CMD`
```bash
FROM ubuntu 
ENTRYPOINT ["sleep"] 
CMD  ["5"]
``` 
## how to override ENTRYPOINT 
1. if you need to override ENTRYPOINT program, then 
1. use `--entrypoint program_name`  
1. `$ docker run --entrypoint sleep2.0 ubuntu-sleeper 10 `   
