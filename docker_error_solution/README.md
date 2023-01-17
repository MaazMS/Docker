## Error response from daemon  removal of container is already in progress 
Error response from daemon: removal of container 9e1e623da3af is already in progress

## solution 
1. sudo systemctl stop docker
2. sudo rm -rf /var/lib/docker/containers/<CONTAINER_ID>
3. sudo systemctl start docker