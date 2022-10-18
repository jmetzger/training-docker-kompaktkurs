# Example nginx with content

## Schritt 1: Simple Example 

```
# das gleich wie cd ~
# Heimatverzeichnis des Benutzers root 
cd
mkdir nginx-test
cd nginx-test
mkdir html
cd html/
nano index.html
```

```
# Text reinschreiben und speichern 
Text, den du rein haben möchtest 
```

```
cd ..
nano Dockerfile 
```
```
FROM nginx:latest
COPY html /usr/share/nginx/html

# nameskürzel z.B. jm1 
docker build -t dockertrainereu/jm1-hello-web . 
docker images

```


## Schritt 2: Push build 

```

# eventually you are not logged in 
# docker login 
# DURCH euren Namen ersetzen -> jm1 
docker push dockertrainereu/jm1-hello-web 
#aus spass geloescht
docker rmi dockertrainereu/jm1-hello-web

```

## Schritt 3: docker laufen lassen

```
# und direkt aus der Registry wieder runterladen 
docker run --name hello-web -p 8080:80 -d dockertrainereu/jm1-hello-web

# laufenden Container anzeigen lassen
docker container ls 
# oder alt: deprecated 
docker ps 

curl http://localhost:8080 


# 
docker rm -f hello-web 
docker rmi dockertrainereu/jm1-hello-web 

```
