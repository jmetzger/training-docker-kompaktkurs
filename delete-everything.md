# Remove unused data (use with care)

```
DOES not always work
```

```
docker system prune 
# Löscht möglicherweise nicht alles

# d.h. danach nochmal prüfen ob noch images da sind
docker images 
# und händisch löschen 
docker rmi <image-name>

```
