# Storage Overview 

## Overview 

```
bind-mount  # not recommended 
volumes
tmpfs 
nfs-mounts
```

## Disadvantages 

```
stored only on one node (besides nfs)
Does not work well in cluster
```

## Alternative for cluster 

```
glusterfs
cephfs 
nfs 

# Stichwort
ReadWriteMany 


```
