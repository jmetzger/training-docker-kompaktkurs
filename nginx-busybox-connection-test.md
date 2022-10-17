# Szenario 1: Testing connection to nginx with busybox 

## Step 1:

```
# nginx - server starten 
docker run --name=nginx-server -d nginx

# Container - IP dieses containers it.
docker inspect nginx-server 

```

## Step 2: 

```
docker run -it --rm busybox sh


```
