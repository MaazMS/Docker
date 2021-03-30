## Docker 
1. Docker have to edition 
    1. community edition 
    1. enterprise edition 
        1. community edition is the set of free docker product.  
        1. enterprise edition is certified and supported with price.  
    
## install docker 
1. https://docs.docker.com/engine/install/ubuntu/  
1. Uninstall old versions  
1. `$ sudo apt-get remove docker docker-engine docker.io containerd runc   `  
1. Install using the convenience script  
1. to copy script.
1.  curl -fsSL https://get.docker.com -o get-docker.sh  
1. To execute the script.  
1. sudo sh get-docker.sh  
1. To install the docker.  
1. sudo docker version.  

## run docker 
1. sudo docker run hello-world  
1. It run hello hello-world   
1. if run `docker run hello-world`  
1. it show `Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/containers/json: dial unix /var/run/docker.sock: connect: permission denied`  
1. solution 
1. Create the docker group if it does not exist
1. `$ sudo groupadd docker`  
1. Add your current user to docker group  
1. `$ sudo usermod -aG docker $USER`  
1. Run the following command or Logout and login again and run (that doesn't work you may need to reboot your machine first).  
1. `$ newgrp docker`  
1. Check if docker can be run without root
1. `$ docker run hello-world`  
1. Reboot if still got error  
1. `$ reboot`  
