**Multi Stage Build**

This is a multistage build example. 

It has an ***app*** folder that contains a simple java maven project. There is a pom file(inside the app folder) which is gonna be used by maven to build the jar.

The Docker file contains two ***FROM*** (multi stage)
```
 - FROM maven:3.5-alpine #this is used to build the jar
 - FROM openjdk:8-alpine #this is used to run the jar
 ```

If you just have the below lines in the Dockerfile
```
FROM maven:3.5-alpine as builder
COPY app /app
RUN cd /app && mvn package
```
It's going to download all the dependencies needed in the pom and the final size of the image is gonna be around 130 MB.

Now then, If you just have the below lines in the Dockerfile
```
FROM openjdk:8-alpine
```
The size of this image is gonna be around 4MB

So, we would think that he final size would be around 234 MB but it won't.

**
The last ***FROM*** will be always the one that is gonna be in the container. The previous ones are just temporary and used to download dependencies, build/compile things for the final result. In this example, it means that the lines that are before the last ***FROM*** are gonna be evaluated but it is just going to keep the jar that is copied into the container
**