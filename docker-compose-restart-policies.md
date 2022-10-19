# Restart Policies 

## what is possible 

```
no: Containers will not restart automatically
on-failure[:max-retries]: Restart the container if it exits with a non-zero exit code and provide a maximum number of attempts for the Docker daemon to restart the container
always: Always restart the container if it stops
unless-stopped: Always restart the container unless it was stopped arbitrarily or by the Docker daemon
```

## Example 

```
# docker-compose.yml 
services:
  web:
    image: 'gitlab/${GITLAB_VERSION}'
    restart: unless-stopped
```

## Reference

 * https://www.baeldung.com/ops/docker-compose-restart-policies 
