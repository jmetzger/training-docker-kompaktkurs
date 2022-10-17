# Images modifizieren interaktiv (Doin't use it) 

## Schritt 1: beispiel 

```
# start clean
docker images | grep ubuntu
# eventually delete images 

# ubuntu starts bash by default 
docker run -it --name=ubuntu-customized ubuntu:latest  
# innerhalb der shell
apt update
apt install telnet 
exit

# to get container-id 
docker container ls -a 
docker commit -m "included telnet" ubuntu-customized ubuntu:latest
docker images

```

## Schritt 2: aufräumen 

```
docker rmi ubuntu:latest 
```
