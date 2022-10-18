# Network 

## Übersicht

```
3 Typen 

o none
o bridge (Standard-Netzwerk) 
o host 

## Additionally possible to install
o overlay (needed for multi-node)

```


## Kommandos 

```
# Netzwerk anzeigen 
docker network ls 

# bridge netzwerk anschauen 
# Zeigt auch ip der docker container an  
docker inspect bridge

# im container sehen wir es auch
docker inspect ubuntu-container 

```

## Test mit eigenem Netz  

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


