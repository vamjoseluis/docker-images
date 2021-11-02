##  Docker commands
**Pull a docker image from DockerHub**
``` 
$ docker pull [app_name]
```
**Pull a specific version of a docker image from DockerHub**
``` 
$ docker pull [app_name]:[tag-name]
```
**Building the Docker image**
``` 
$ docker build -t [image-name:tag-name]
```
e.g.
```
$ docker build -t apache-centos:2.0
```



## Image commands
**Get list of images avilable**
```
$ docker images
```
**Delete an image**
```
$ docker rmi [image-name:tag-name]
```
**See the history of an image**
```
docker history -H [image-name:tag-name] --no-trunc
```


## Container commands
**Create a container**
```
$ docker run -d -p [local-port:container-port]  --name [container-name] [image-name:tag-name]
```
e.g. 
```
$ docker run -d -p 80:80  --name centos-instance apache-centos:2.0
```
**Stop container**
```
$ docker stop [container-name]
```
**Start container**
```
$ docker start [container-name]
```
**Restart container**
```
$ docker restart [container-name]
```
**Delete a container**
```
$ docker rm -fv [container-name]
```
**Delete all container**
```
$ docker ps -q | xargs docker rm -f
```
**Login into the container**
```
$ docker exec -ti [container-name] bash
```
**Login into the container with a specific user**
```
$ docker exec -u [user_name] -ti [container-name] bash
```
**Get container's details/information**
```
$ docker inspect [container-name]
```
**Check how many resources is consuming a container**
```
$ docker stats [container-name]
```
**Get the logs of an image**
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
The below arguments can be used in the Dockerfile.
- **FROM**
It sets an initial ***image*** (base image) for subsequent instructions. It can be started from scratch too.
e.g.
```
FROM centos
```
e.g.
```
FROM scratch
```
- **RUN**
It will execute any commands in a new layer in top of the current image.
e.g.
```
#command to install apache in centos
yum install httpd -y
```
- **COPY/ADD**
Copy a file or dir from the src to the specified container's path
e.g.
```
COPY run.sh /run.sh
```
- **ENV**
It sets the environment variable <key> to the value <value>
e.g.
```
ENV environment=dev
```
- **WORKDIR**
To set a new path as current work dir
e.g.
```
WORKDIR /var/www/html
```
- **EXPOSE**
To indicate what port(s) are gonna be available. It can be TCP or UCP, and TCP is the default port.
It doesn't publish the port. To publish the port you have to use -p while running the container
- **LABEL**
It adds metadata to the image
- **USER**
It sets the User (UID) and optionally the user group to use when running the image.
- **VOLUME**
It creates a mount point wth the specified name and marks it as holding externally volumes from host or other containers.
- **CMD**
It provides defaults for an executing container. The default can include an executable. There can be only one CMD per Dockerfile. If there are more than one, then the last one will take effect.
