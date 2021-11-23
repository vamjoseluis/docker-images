##  Docker commands
**Pull a docker image from DockerHub**
```sh 
$ docker pull [app_name]
```
**Pull a specific version of a docker image from DockerHub**
```sh 
$ docker pull [app_name]:[tag-name]
```
**Building the Docker image**
```sh 
$ docker build -t [image-name:tag-name]
```
e.g.
```sh
$ docker build -t apache-centos:2.0
```
**list of volumenes**
```sh
$ docker volume ls
```
**delete a volume**
```sh
$ docker volume rm [volume-name]
```
e.g.
```sh
$ docker volume rm 3c2341f7c59a7275b98536a723395928100491555efed5af14e0c398e9a4b731
```
**Delete dangling volumenes**
```bash
$ docker volume ls -f dangling=true -q | xargs docker volume rm
```
**To find where Docker is installed** (it works just for linux)
```bash
$ docker info | grep -i root
```
In case you are using Mac, You can use either of the two commands.
```bash
$ docker run -it --rm --privileged --pid=host alpine:edge nsenter -t 1 -m -u -n -i sh
```

```bash
$ docker run -it --rm --privileged --pid=host justincormack/nsenter1
```

## Image commands
**Get list of images avilable**
```bash
$ docker images
```
**Delete an image**
```bash
$ docker rmi [image-name:tag-name]
```
**See the history of an image**
```bash
docker history -H [image-name:tag-name] --no-trunc
```


## Container commands
**Create a container**
```bash
$ docker run -d -p [local-port:container-port]  --name [container-name] [image-name:tag-name]
```
e.g. 
```bash
$ docker run -d -p 80:80  --name centos-instance apache-centos:2.0
```
**Stop container**
```bash
$ docker stop [container-name]
```
**Start container**
```bash
$ docker start [container-name]
```
**Restart container**
```bash
$ docker restart [container-name]
```
**Delete a container**
```bash
$ docker rm -fv [container-name]
```
**Delete all container**
```bash
$ docker ps -q | xargs docker rm -f
```
**Login into the container**
```bash
$ docker exec -ti [container-name] bash
```
**Login into the container with a specific user**
```bash
$ docker exec -u [user_name] -ti [container-name] bash
```
**Get container's details/information**
```bash
$ docker inspect [container-name]
```
**Check how many resources is consuming a container**
```bash
$ docker stats [container-name]
```
**Get the logs of an image**
```bash
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
```bash
FROM centos
```
e.g.
```bash
FROM scratch
```
- **RUN**
It will execute any commands in a new layer in top of the current image.
e.g.
```bash
#command to install apache in centos
yum install httpd -y
```
- **COPY/ADD**
Copy a file or dir from the src to the specified container's path
e.g.
```bash
COPY run.sh /run.sh
```
- **ENV**
It sets the environment variable <key> to the value <value>
e.g.
```bash
ENV environment=dev
```
- **WORKDIR**
To set a new path as current work dir
e.g.
```bash
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
