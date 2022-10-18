# Network 

## 1. Übersicht

```
3 Typen 

o none
o bridge (Standard-Netzwerk) 
o host 

## Additionally possible to install
o overlay (needed for multi-node)

```


## 2. Kommandos 

```
# Netzwerk anzeigen 
docker network ls 

# bridge netzwerk anschauen 
# Zeigt auch ip der docker container an  
docker inspect bridge

# im container sehen wir es auch
docker inspect ubuntu-container 

```

## 3. Test mit eigenem Netz (bridged) 

### Schritt 1: Netzwerk erstellen 

```
docker network create -d bridge app_net 
docker inspect app_net 
```


### Schritt 2: Netzwerk testen  

```
docker run -dit --name alpine1 --network app_net alpine ash  
docker run -dit --name alpine2 --network app_net alpine ash
docker run -dit --name alpine3 alpine ash 

# ip rausfinden 
docker inspect alpine3 | grep -i ipaddress 

docker exec -it alpine1 ash
/ # ping -c2 alpine2 
/ # ping -c2 alpine3 
/ # ping -c2 <ip-addr>
/ # exit

docker exec -it alpine3 ash
/ # ping -c2 alpine1 
/ # ping -c2 <ip-addresse>

```

### Schritt 3: Test von container mit 2 Netzwerken 

```
docker run -dit --name alpine4 alpine ash 
docker network connect app_net alpine4 
docker inspect alpine4

docker exec -it alpine4 ash 
/# ping alpine1
# alpine3 lässt soch nicht mit Namen anpingen, weil mit der der default -> bridge verbunden
# dort gibt es keine Namensauflösung 
/# ping alpine3
/# ping <ip-address-alpine3>
```


## 4. Test mit Host-Netz 

```
# start first container 
docker run --network host -d nginx 
# will bind to port 80  
lsof -i 
# start second container 
docker run --network host -d nginx 
# Will run only the first
docker container ls -a 

CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                     PORTS     NAMES
acaffd1c8ac9   nginx     "/docker-entrypoint.…"   2 minutes ago    Exited (1) 2 minutes ago             priceless_kapitsa
476a52395eb9   nginx     "/docker-entrypoint.…"   2 minutes ago    Up 2 minutes                         focused_buck

docker rm -f ac 47 

# und jetzt ist der Server von aussen erreichbar 

```



## Eigenes Netz erstellen 

```
docker network create -d bridge test_net 
docker network ls 

docker container run -d --name nginx --network test_net nginx
docker container run -d --name nginx_no_net --network none nginx 

docker network inspect none 
docker network inspect test_net 

docker inspect nginx 
docker inspect nginx_no_net 

```

## Netzwerk rausnehmen / hinzufügen 

```
docker network disconnect none nginx_no_net
docker network connect test_net nginx_no_net 

## Das Löschen von Netzwerken ist erst möglich, wenn es keine Endpoints 
## d.h. container die das Netzwerk verwenden 
docker network rm test_net 
```


