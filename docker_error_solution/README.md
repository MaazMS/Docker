## Error response from daemon  removal of container is already in progress 
Error response from daemon: removal of container 9e1e623da3af is already in progress

## solution 
1. sudo systemctl stop docker
2. sudo rm -rf /var/lib/docker/containers/<CONTAINER_ID>
3. sudo systemctl start docker 


## docker permission denied  
1. create , delete and update file inside docker return error permission denied   

solution 
1. first check user inside docker using command `whoami`  
2. check the file and folder permission using command `ls -a`  
3. if you are not root user then loging the root user 
4. root user login command is `docker exec -it -u root contianer_name  /bin/bash` 
