# Install docker (ubuntu) with snap

## Step 1: install 

```
sudo su -
snap install docker
```

## Step 2: Validate if service is running ? 

```
systemctl status snap.docker.dockerd.service
# oder (aber veraltet) 
service snap.docker.dockerd status
```

## Optional: Find the name of the service 

```
# for information retrieval 
snap info docker
systemctl list-units
systemctl list-units -t service
systemctl list-units -t service | grep docker
```

```
systemctl stop snap.docker.dockerd.service
systemctl status snap.docker.dockerd.service
systemctl start snap.docker.dockerd.service 

# wird der docker-dienst beim nächsten reboot oder starten des Server gestartet ? 
systemctl is-enabled snap.docker.dockerd.service

```
