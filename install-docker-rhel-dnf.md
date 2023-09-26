# Install docker with dnf on Rocky 9 

## Walkthrough 

```
# as root
dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
dnf install docker-ce docker-ce-cli containerd.io docker-compose-plugin
# aktivieren und starten, das gleiche wie enable & start 
systemctl enable --now docker
```



## Ref:

  * https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-rocky-linux-8

