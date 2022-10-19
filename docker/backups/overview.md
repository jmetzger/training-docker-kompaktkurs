# How to backup in Docker 

## What to backup ? 

  * Sicherung meiner docker-compose - Projekte 
    * z.B Versionsverwaltung (git). 
  * Sicherung von Volumes 
  * Sicherung von Datenbank-Daten 

## gitlab 

  * Sicherungstools 
  * Sinnvoll generell wenn diese zur Verfügung stehen. 

## Walkthrough (backup) 

```
# Daten erstellt 
docker volume create testdata 

# Datenbefüllung simulieren 
docker run -it -v testdata:/testdata ubuntu cp -a /etc /testdata

# Sichern 
docker run --rm -v /backups/volumes:/backup -v testdata:/data:ro  debian:stretch-slim bash -c "cd /data && /bin/tar -czvf /backup/test-data.tar.gz  ."
cd /backups/volumes 
ls -la 
# hier dann test-data.tar.gz 

```

## Walkthrough (Restore) 

```
docker run --rm \
        -v /backups/volumes:/backup \
        -v testdata:/data \
        debian:stretch-slim bash -c "cd /data && /bin/tar -xzvf /backup/test-data.tar.gz"
```

## Reference 

  * https://www.laub-home.de/wiki/Docker_Backup_und_Restore_-_eine_kleine_Anleitung

