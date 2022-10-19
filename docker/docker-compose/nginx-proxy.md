# Nginx-proxy verwenden für mehrere Domains auf einem Server (subdomains) 

## Walktrough 

```
cd 
mkdir jwilder-nginx-proxy
cd jwilder-nginx-proxy
nano docker-compose.yml 
```

```
version: '3'

services:
  nginx-proxy:
    image: jwilder/nginx-proxy
    ports:
      - "80:80"
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro

  whoami:
    image: jwilder/whoami
    environment:
      - VIRTUAL_HOST=whoami.local,whoami.training.local
```

```
docker compose up -d 
```

```
# Eintrag in meinem Desktop-Client gemacht 
# Windows->System32->drivers->etc->hosts 
# mit notepad++ -> als Administrator starten 
# ip meines server 
192.168.56.107 whoami.training.local  whoami 
```

```
# im Browser achtung: http:// verwenden 
http://whoami.training.local 
```
