# Install docker (ubuntu) with snap

## Step 1: install 

```
sudo su -
snap install docker
```

## Step 2: Validate if service is running and enabled ? 

```
systemctl status snap.docker.dockerd.service
# oder (aber veraltet) 
service snap.docker.dockerd status

systemctl is-enabled snap.docker.dockerd.service 
# Dienst aktivieren (er wird dann auch beim nächsten Boot gestartet) - Windows Autostart 
systemctl enable snap.docker.dockerd.service 

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

## Optional: Access to docker-daemon aus unprvileged user 

```
sudo addgroup --system docker
sudo adduser $USER docker
# lädt die neue Gruppe in den User hinein 
newgrp docker
sudo snap disable docker
sudo snap enable docker


```
