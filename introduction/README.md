## Introduction    
1. What is docker?  
    Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers.
3.  why we need docker ?  
Example   
    Requirement to setup end-to-end an applicattion with different technology like web server using nodejs, database mongoDB  
    messages system radis and orchestration ansible.  
    
1. Requirement 
    1. compatibility on os was issues we ensure that all different technology compatible with version of os..  
    1. where certain version of the services with not compatible to so.  
    1. we look the os with comaptible to all services 
    1. we check the compatibiity betweem the services and libraies and dependency on the os.  
    1. we have issue where one service require one version of dependent library and other service require another version  
    of dependency.  
    1. The archtecture is chagne over time.  
    1. upgate version , chnage database version etc.  
    1. Every time someting is chnage we had to go through same process of checking comaptbiity beween these version and there component.  
    1. This is compatibilty matrix isssue usually refered to os.  
    
1. Every time new developer onbord we found it really difficult to setup a new environemt.  
1. Follow the large instrcution to setup the envirmrnyt.  
1. There are differnt environrmt suuch as testing, production, development.  
1. So building and shiping the application of diffenet environt is very difficult.  


1. We need compatibility issue 
1. modify and chnage the compnet without effecting other component and even modify underlying os as required.  

1. On docker i was able to run each compnet in seprate container with it's own dependency and it's own libray on same vm or os  
within seprate enviroment or container.   
   
1. containeruze applications run seach services with its own dependency in seprate containers 

1. What are Containers?  
    1. conatiner are compalty islolated environment can have own process , network interface,  mounts all share same os kernal.  
    1. Docker utilize LXC container.  
    1.  os kernal is reponsible to interaction underlying hardware.  

1. What is os that do not share the same kernal?  
   windowns and you won't be able to run a windows based container on docker host with linux on it. 
   for that you are requerid a docker on windows server. 
   when you install docker on window and run linux container on windows you are not really runing a linux container on windows.  
   windows run linux conatiner on linux virtual machine under the hood.  
   so it's really linux container on linux virtual machine on windows. 

## container vs virtual machine 
https://docs.microsoft.com/en-us/virtualization/windowscontainers/about/containers-vs-vm
![](https://www.weave.works/assets/images/bltb6200bc085503718/containers-vs-virtual-machines.jpg)   
![](https://docs.microsoft.com/en-us/virtualization/windowscontainers/about/media/container-diagram.svg)  
![](https://docs.microsoft.com/en-us/virtualization/windowscontainers/about/media/virtual-machine-diagram.svg)  
1. Docker is not meant to virtualize and run differnt os and kernal on the same hardware, the main purpose of docker is to package and container as application  
and to ship them and to run them anywhere any time as many time as you want.    

container | virtual machine  
|---|---|  
lowe utilization | heigh utilization  
low disk size | heigh disk size   

## container vs image 
1. An image is a package or template. it is used to create one and more containers 
1. containers are running instances of images   

## Docker in devops  
https://bigdatapath.wordpress.com/2020/01/17/what-is-devops-how-is-devops-different-from-traditional-it/
![](https://bigdatapath.files.wordpress.com/2020/01/2-2.png)  
1. tradionally developer develop an application then it hand to ops team to deploy and manage it in production enviroment, 
they do that providing a set of instrcution such as infomation about how to host must be stup, what are prerquisties are to be  
installed on the host and how dependency are to be configure etc.  
1. ops team is not develop the application ,the are deploying,operate,monitor, release application if they find issue they worked on developers  
to reslove it.  
1. Using docker the developer and operation teams work hand-in-hand to transform the guide into a docker file with both of   
their requeriment.`dockerfile`  
1. This docker file is create docker image.  
1. This image is run any host with docker install.  
1.  It run same way in any where.  

