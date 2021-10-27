# This is an example of a docker file with Centos and Apache

- It runs apache through a sh file on port 80, so the port must be mapped to the port desired.
- It contains a basic html project (business) which is copied to /var/www/html.

## How to run it.

### Building the Docker image
``` 
$ docker build -t [image-name:tag-name]
```
e.g.
```
$ docker build -t apache-centos:2.0
```
### Checking if the image is available
```
$ docker images
```

### Run the image
```
$ docker run -d -p [local-port:container-port]  --name [container-name] [image-name:tag-name]
```
e.g. 
```
$ docker run -d -p 80:80  --name centos-instance apache-centos:2.0
```

##  Useful Commands 
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
### Check how many resources is consuming the container
```
$ docker stats [container-name]
```


## Docker - Best Practices
- Ephemeral. The service should be easy to destroy
- One service per image/container (by instace apache and mysql)
- Add undesirable files to the .dockerignore to reduce image's size
- Try to use the less layers as you can
- Split arguments in different lines to make it more redeable
- Not to install unnecessary packages
- User LABELS to add metadata