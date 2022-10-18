# Storage Volumes 

## Storage volumes verwalten 

```
docker volume ls
docker volume create test-vol
docker volume ls
docker volume inspect test-vol
```

## Storage volumes in container einhängen

```
# Schritt 1
docker run -it --name=container-test-vol --mount target=/test_data,source=test-vol ubuntu bash
1234ad# touch /test_data/README 
exit
# stops container 
docker container ls -a
```

```
# Schritt 2 
Inhalt im Filesystem betrachten.
docker volume inspect test-vol 
# ziehen wir den pfad raus 
ls -la /var/snap/docker/common/var-lib-docker/volumes/test-vol/_data
cat /var/snap/docker/common/var-lib-docker/volumes/test-vol/_data/README 
```

```
# Schritt 3:
# create new container and check for /test_data/README 
docker run -it --name=container-test-vol2 --mount target=/test_data_neu,source=test-vol ubuntu bash
ab45# ls -la /test_data_neu/README 
```

## Storage volume löschen 

```
# Zunächst container löschen 
docker rm container-test-vol 
docker rm container-test-vol2
docker volume rm test-vol
```
