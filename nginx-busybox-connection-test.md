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
# Assuming nginx-server has pod-ip 172.17.0.2 
# connects to sh by default 
docker run -it --rm busybox
/ # ping 172.17.02 
/ # wget -O - http://172.17.0.2 

```
