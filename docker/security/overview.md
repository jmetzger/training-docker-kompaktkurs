# Security Overview 

## Run container under specific user: 

```
# user with id 40000 does not need to exist in container 
docker run -it -u 40000 alpine 

# user kurs needs to exist in container (/etc/passwd) 
docker run -it -u kurs alpine 

```

## Default capabilities 

  * Set everytime a new container is started as default 
  * https://github.com/moby/moby/blob/master/profiles/seccomp/default.json


## Run container with less capabilities 

```
cd
mkdir captest
cd captest 
```

```
nano docker-compose.yml 
```

```
services: 
  alpine1:
    image: alpine 
    cap_drop:
      - CHMOD 
      - CHOWN
```

```
docker compose up .d 
docker exec -it captest_alpine1_1 ash
/ # touch /tmp/foo && chmod o=rwx /tmp/foo 
```

```
docker compose down 
```


## Reference:

  * https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html
  * man capabilities
