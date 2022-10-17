# Images modifizieren interaktiv 

## Schritt 1: beispiel 

```
# ubuntu starts bash by default 
docker run -it --name=ubuntu-customized ubuntu:latest  
# innerhalb der shell
apt update
apt install telnet 
exit

docker images
docker commit ubuntu-customized ubuntu:latest
docker images

```

## Schritt 2: aufräumen 

```
docker rmi ubuntu:latest 
```
