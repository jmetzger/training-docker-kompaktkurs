# Deploy Private Registry Server 

## Walkthrough 

```
docker run -d -p 5000:5000 --restart=always --name registry registry:2
docker pull ubuntu:16.04
docker tag ubuntu:16.04 localhost:5000/my-ubuntu
docker push localhost:5000/my-ubuntu

docker image remove ubuntu:16.04
docker image remove localhost:5000/my-ubuntu
docker pull localhost:5000/my-ubuntu


```


## Reference 


  *  https://docs.docker.com/registry/deploying/
