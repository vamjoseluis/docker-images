##  Docker commands Commands 
### Pull a docker image form docker hub
``` 
$ docker pull [app_name]
```
### Pull a specific version of a docker image form docker hub
``` 
$ docker pull [app_name]:[tag-name]
```
### Building the Docker image
``` 
$ docker build -t [image-name:tag-name]
```
e.g.
```
$ docker build -t apache-centos:2.0
```



## Images commands
### Get list of images avilable
```
$ docker images
```
### Delete an image
```
$ docker rmi [image-name:tag-name]
```
### See the history of an image
```
docker history -H [image-name:tag-name] --no-trunc
```


## Container commands
### Create a container
```
$ docker run -d -p [local-port:container-port]  --name [container-name] [image-name:tag-name]
```
e.g. 
```
$ docker run -d -p 80:80  --name centos-instance apache-centos:2.0
```
### Stop container
```
$ docker stop [container-name]
```
### Start container
```
$ docker start [container-name]
```
### Restart container
```
$ docker restart [container-name]
```
### Delete a container
```
$ docker rm -fv [container-name]
```
### Delete all container
```
$ docker ps -q | xargs docker rm -f
```
### Login into the container
```
$ docker exec -ti [container-name] bash
```
### Login into the container with a specific user
```
$ docker exec -u [user_name] -ti [container-name] bash
```
### Get container's details/information
```
$ docker inspect [container-name]
```
### Check how many resources is consuming a container
```
$ docker stats [container-name]
```
### Get the logs of an image
```
$ docker logs -f [container-name]
```



## Docker - Best Practices
- Ephemeral. The service should be easy to destroy
- One service per image/container (by instace apache and mysql)
- Add undesirable files to the .dockerignore to reduce image's size
- Try to use the less layers as you can
- Split arguments in different lines to make it more redeable
- Not to install unnecessary packages
- User LABELS to add metadata


## Dockerfile Arguments
- FROM
- RUN
- COPY/ADD
- ENV
- WORKDIR
- EXPOSE
- LABEL
- USER
- VOLUME
- CMD
