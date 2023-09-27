# Docker Kompaktkurs 

## Agenda 

  1. Docker-Grundlagen 
     * [Übersicht Architektur](architektur.md)
     * [Was ist ein Container ?](container.md)
     * [Was sind container images](container-images.md) 
     * [Container vs. Virtuelle Maschine](container-vs-vm.md)
     * [Was ist ein Dockerfile](dockerfile.md) 
  
  1. Docker-Installation
     * [Installation Docker unter Ubuntu mit snap](install-ubuntu-snap.md)
     * [Installation Docker unter SLES 15](install-sles15-zypper.md)
     * [Installation Docker unter Ubuntu mit Docker Repo](install-docker-ubuntu-apt.md)
     * [Installation Docker unter RHEL/Rocky mit Docker Repo](install-docker-rhel-dnf.md)
  
  1. Docker-Befehle 
     * [Docker Grundlagen run](docker-befehle.md)
     * [Die einzelnen Image-Schichten anschauen](docker-history.md) 
     * [Logs anschauen - docker logs - mit Beispiel nginx](docker-logs-nginx.md)
     * [docker run](docker-run.md)
     * [Docker container/image stoppen/löschen](container-image-delete.md)
     * [Docker containerliste anzeigen](container-liste.md)
     * [Docker nicht verwendete Images/Container löschen](delete-everything.md)
     * [Docker container analysieren](docker-inspect.md)
     * [Docker container in den Vordergrund bringen - attach](/docker/docker-attach.md) 
     * [Aufräumen - container und images löschen](prune-container-images.md)
     * [Nginx mit portfreigabe laufen lassen](docker-example-nginx.md)  
     * [docker-commit](docker-commit.md)
     * [images taggen und tags löschen](docker-tag.md)
  
  1. Docker - Szenarien 
     * [Verbindung zu nginx mit anderem Container testen](nginx-busybox-connection-test.md) 

  1. Dockerfile - Examples 
     * [Ubuntu mit hello world](ubuntu-hello-world.md)
     * [Ubuntu mit ping](ubuntu-ping.md) 
     * [Nginx mit content aus html-ordner](nginx-html-content.md)
     * [ssh server](ubuntu-ssh-server.md)
  
  1. Docker-Container Examples 
     * [2 Container mit Netzwerk anpingen](2-containers-with-network-ping.md)
     * [Container mit eigenem privatem Netz erstellen](container-with-own-bridge.md)  
  
  1. Container-Image bei Laufzeit konfigurieren 
     * [Container-Image bei Laufzeit konfigurieren](container-env.md)
  
  1. Docker-Daten persistent machen / Shared Volumes 
     * [Überblick](storage-overview.md) 
     * [Volumes](storage-volumes.md) 
     * [bind-mounts](docker-bind-mount.md)
  
  1. Docker-Netzwerk 
     * [Netzwerk](network.md)
     * [Internes Netz ohne Internetzugang aufsetzen](docker/docker-compose/setup-internal-net.md)
  
  1. Docker Compose
     * [yaml-format](yaml-format.md)
     * [Ist docker-compose installiert?](docker-compose-installed.md) 
     * [Example with Wordpress / MySQL - Good !](example-wordpress-mysql.md)
     * [Example with Ubuntu and Dockerfile](example-docker-compose-ubuntu-build.md)
     * [Logs in docker - compose](docker-compose-logs.md)
     * [docker-compose und replicas](docker-compose-replicas.md)
     * [restart policies](docker-compose-restart-policies.md)
  
  1. Docker Swarm 
     * [Docker Swarm Beispiele](docker-swarm-examples.md)

  1. Docker Registry
     * [Privater Registry Server](private-registry-server.md)
     
  1. Docker Reverse Proxy (vorgeschaltet) 
     * [Docker mit Reverse Proxy verwenden](/docker/docker-compose/nginx-proxy.md)
     
  1. Docker Security 
     * [Docker Security](docker/security/overview.md)

  1. Docker Monitoring
     * [Docker Monitoring - cAdvisor/Prometheus](/docker/monitoring/cadvisor-prometheus.md)
     * [Prometheus Funktionsweise](/prometheus/overview.md) 

  1. Docker - Dokumentation 
     * [Vulnerability Scanner with docker](https://docs.docker.com/engine/scan/#prerequisites)
     * [Vulnerability Scanner mit snyk](https://snyk.io/plans/)
     * [Parent/Base - Image bauen für Docker](https://docs.docker.com/develop/develop-images/baseimages/)
    
  1. Linux und Docker Tipps & Tricks allgemein 
     * [Auf ubuntu root-benutzer werden](sudo.md)
     * [IP - Adresse abfragen](ip-a.md)
     * [Hostname setzen](hostname.md)
     * [Läuft der ssh-server](ssh-running.md)

  1. VirtualBox Tipps & Tricks 
     * [VirtualBox 6.1. - Ubuntu - Entwicklungsserver für Docker aufsetzen ](virtualbox-ubuntu.md)
     * [VirtualBox 6.1. - Shared folder aktivieren](virtualbox-shared-folders.md)

  1. Kubernetes - Überblick
     * [Warum Kubernetes, was macht Kubernetes](warum-kubernetes.md) 
     * [Aufbau Allgemein](/kubernetes/architecture.md)


## Backlog 

  1. Linux und Docker Tipps & Tricks allgemein 
     * [Proxy für Docker setzen](proxy-docker.md)
     * [vim einrückung für yaml-dateien](/vim/vim-yaml.md)
     * [YAML Linter Online](http://www.yamllint.com/)
     * [Basis/Parent - Image erstellen](docker-base-image.md)
     * [Eigenes unsichere Registry-Verwenden. ohne https](insecure-registry.md)
