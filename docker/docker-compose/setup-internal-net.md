# Setup internal net 

## Why ? 

  * When containers are in an internal net, they are not able to reach the outside world (aka internet) 

## Setup / Walkthrough 

```
mkdir internal
cd internal/
nano docker-compose.yml
```

```
docker compose up -d
docker network ls
docker compose ps
# Update will not work now 
docker exec -it internal-partner1-1 bash
/ # apt update
```

## Connect to the outside world 

```
docker network create -d bridge app-public
docker network connect app-public internal-partner1-1
# Now it works 
docker exec -it internal-partner1-1 bash
/ # apt update
```
