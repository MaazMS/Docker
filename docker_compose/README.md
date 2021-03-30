# docker compose   
1. Using docker compose we create configuration file in yaml format is called `docker-compose.yaml`   
1. Put different services and in a docker compose file and run `docker-compose up`.  
1. It is applicable to run docker in single host.   
1. docker compose is a tool for defining and running multi-container Docker applications.   

## Example without docker   
1. This is the example for voting app. 
1. Component for voting app is voting app written in python, Redis is in-memory db, worker , database in postgres, 
front end is node js.  
1. To run this application using docker without docker compose we run command.  
    1. docker run -d --name = redis redis    
    1. docker run -d --name = db postgres:9.4 --link db:db  result-app  
    1. docker run -d --name = vote -p 5000:80 --link redis:redis voting-app  
    1. docker run -d --name = result -p 5000:80  
    1. docker run -d --name = worker --link db:db --link redis:redis worker   
    
## docker compose example
1. The above applicaton using docker is to much time, difficult to link the application    
1. use docker compose it is easy to use and single yaml and manage every thing by command `docker-compose up`  
```yaml
redis : 
  image : redis 
db :
  image : postgres:9.4
vote:     
  image : voting-app 
  ports : 
     - 5000:80
  links :
     - redis
result :
   image : result-app
   ports :
      - 5000:80
      links :
         - db
worker:
   image : worker
   links :
      - redis
      - db 
``` 
## docker compose build example 
1. if we use docker build instead of pulling image in dockerhub. 
1. we replace `image` to `build` and specify the location of directory which contain application contain and docker file instruction.  
1. Then it build docker image,
```yaml
redis : 
  image : redis 
db :
  image : postgres:9.4
vote:
   build : ./voting-app 
  ports : 
     - 5000:80
  links :
     - redis
result :
   build : ./result-app
   ports :
      - 5000:80
      links :
         - db
worker:
   build : ./worker
   links :
      - redis
      - db 
``` 
## Compose versions
1. Following table captures the main differences between Compose versions:  
  

Feature | Compose v1 | Compose v2 | Compose v3 | 
---|---|---|---| 
Docker engine version	| 1.9.1+ |1.10.0+ |1.13.0+
Compose version | Compose up to 1.6.x | Compose 1.6.0+ | Compose 1.10.0+   
Connect containers | Bridge network, need links | Overlay supported, networks can be used to connect containers | Overlay supported, networks can be used to connect containers  
Volume | No named volume | Named volume supported | Named volume supported  
Swarm capability | Older swarm | Older swarm | Swarm mode  
Deploy section	| No deploy section | No deploy section	 | Deploy section with replica present  


## votingapp in compose v1  
1. Following is the votingapp in compose v1 format. This establishes container connectivity using links and can be  
   deployed in a standalone node or in a cluster using old swarm mode.  
```yaml
vote:
    image: docker/example-voting-app-vote:latest
    environment:
      - "constraint:node==swarm-agent-753F9D8C000000"
    ports:
      - "5000:80"
    links:
      - redis

redis:
    image: redis:alpine
    environment:
      - "constraint:node==swarm-agent-753F9D8C000000"
    ports: ["6379"]

worker:
    image: docker/example-voting-app-worker:latest
    environment:
      - "constraint:node==swarm-agent-753F9D8C000000"
    links:
      - redis
      - db

db:
    image: postgres:9.4
    ports: ["5432"]
    environment:
      - "constraint:node==swarm-agent-753F9D8C000000"

result:
    image: tmadams333/example-voting-app-result:latest
    ports:
      - "5001:80"
    environment:
      - "constraint:node==swarm-agent-753F9D8C000000"
    links:
      - db
```   
1. Following command can be used to deploy: 
`docker-compose up -d`  
   
## votingapp in compose v2 
1. Following is the votingapp in compose v2 format. This establishes container connectivity using networks and can be   
   deployed in standalone node or in cluster using old swarm mode. Containers connected through networks can be deployed   
   in separate nodes and they can talk through overlay network here.  
   
```yaml
version: "2"

services:
  vote:
    image: docker/example-voting-app-vote:latest
    labels:
     - "com.example.description=Vote"
    ports:
      - "5000:80"
    networks:
      - front-tier
      - back-tier

  redis:
    image: redis:alpine
    ports: ["6379"]
    networks:
      - back-tier

  worker:
    image: docker/example-voting-app-worker:latest
    networks:
      - back-tier

  db:
    image: postgres:9.4
    ports: ["5432"]
    labels:
     - "com.example.description=Postgres Database"
    networks:
      - back-tier

  result:
    image: tmadams333/example-voting-app-result:latest
    ports:
      - "5001:80"
    networks:
      - front-tier
      - back-tier

networks:
  front-tier:
  back-tier:
```

1. Following command can be used to deploy:
   `docker-compose up -d`  
   
## votingapp in compose v3 
1. Following is the votingapp in compose v3 format. This establishes container connectivity using networks and can be    
   deployed in standalone node or in new swarm mode. This compose format has the deploy section that controls deployment  
   parameters like number of replicas, constraints etc.  
   
```yaml
version: "3"
services:

  redis:
    image: redis:alpine
    ports:
      - "6379"
    networks:
      - frontend
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure
  db:
    image: postgres:9.4
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - backend
    deploy:
      placement:
        constraints: [node.role == manager]
  vote:
    image: dockersamples/examplevotingapp_vote:before
    ports:
      - 5000:80
    networks:
      - frontend
    depends_on:
      - redis
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
      restart_policy:
        condition: on-failure
  result:
    image: dockersamples/examplevotingapp_result:before
    ports:
      - 5001:80
    networks:
      - backend
    depends_on:
      - db
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure

  worker:
    image: dockersamples/examplevotingapp_worker
    networks:
      - frontend
      - backend
    deploy:
      mode: replicated
      replicas: 1
      labels: [APP=VOTING]
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
      placement:
        constraints: [node.role == manager]

networks:
  frontend:
  backend:

volumes:
  db-data:
```

1. Following command can be used to deploy:
   `docker-compose up -d`  