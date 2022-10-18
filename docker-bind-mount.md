# Example 

```
 docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source=/srv,target=/app \
  nginx:latest
```
