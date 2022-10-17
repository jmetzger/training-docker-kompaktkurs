# Ubuntu mit ping 

## Schritt 1: Container bauen 


```
mkdir myubuntu 
cd myubuntu/
```

```
# nano Dockerfile
FROM ubuntu:latest
RUN apt-get update; apt-get install -y inetutils-ping
CMD ["/bin/bash"]
```

```
docker build -t myubuntu .
docker images
# -t wird benötigt, damit bash WEITER im Hintergrund im läuft.
# auch mit -d (ohne -t) wird die bash ausgeführt, aber "das Terminal" dann direkt beendet 
# -> container läuft dann nicht mehr 
```

## Schritt 1b: Dockerfile aufhübschen (best practice) 


```
FROM ubuntu:latest
RUN apt-get update && \
  apt-get install -y inetutils-ping && \
  rm -rf /var/lib/apt/lists/*
```

```
# With comments 
FROM ubuntu:latest
# Better use && and new lines 
# RUN apt-get update; apt-get install -y inetutils-ping
RUN apt-get update && \
  apt-get install -y inetutils && \
  rm -rf /var/lib/apt/lists/*

# is not needed, because CMD["bash"] is default in ubuntu:latest 
# CMD ["/bin/bash"]
```


## Schritt 2: Container testen 


```
docker run -d -t --name container-ubuntu myubuntu
docker container ls
# in den container reingehen mit dem namen des Containers: myubuntu 
docker exec -it myubuntu bash
ls -la
```

## Schritt 3: ping von neuem container zu altem Container 

```
# Zweiten Container starten
docker run -d -t --name container-ubuntu2 myubuntu 

# docker inspect to find out ip of other container 
# 172.17.0.3 
docker inspect <container-id>

# Ersten Container -> 2. anpingen 
docker exec -it container-ubuntu bash 
# Jeder container hat eine eigene IP 
ping 172.17.0.3

 
```
