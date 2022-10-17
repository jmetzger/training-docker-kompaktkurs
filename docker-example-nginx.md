# Beispiel nginx 

## Schritt 1: Container erstellen 

```
# Container 1 
docker run --name test-nginx -d -p 8080:80 nginx
# Container 2 
docker run --name test-nginx2 -d -p 80:80 nginx 
```

## Schritt 2: Tests durchführen 

```
docker container ls
lsof -i
cat /etc/services | grep 8080
# Mit Browser in Remote Desktop testen: 192.168.56.104:8080 
# oder 
curl http://localhost:8080
docker container ls
```

## Schritt 3: Container stoppen und probieren zu erreichen 

```
# wenn der container gestoppt wird, keine ausgabe mehr, weil kein webserver
docker stop test-nginx 
# Mit Browser in Remote Desktop testen: 192.168.56.104:8080 
# oder
curl http://localhost:8080
```
