# This is an example of a Docker file with Centos and Apache

- It runs apache through a sh file (run.sh) on port 80 (container port), so the port must be mapped to the port desired while running the container (-p [local-port:container-port]).
- It contains a basic html project (business) which is copied to /var/www/html.

## How to run it.

### Build the Docker image
``` 
$ docker build -t [image-name:tag-name]
```
e.g.
```
$ docker build -t apache-centos:2.0
```
### Check if the image is available
```
$ docker images
```

### Start a container
```
$ docker run -d -p [local-port:container-port]  --name [container-name] [image-name:tag-name]
```
e.g. 
```
$ docker run -d -p 80:80  --name centos-instance apache-centos:2.0
```