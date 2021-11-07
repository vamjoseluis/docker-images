#To compile a jar file, It set builder as alias to the stage
FROM maven:3.5-alpine as builder

#Copy app folder into the container(to /app path)
COPY app /app

#go into the /app folder and build the jar
RUN cd /app && mvn package

#With this FROM we are going to discard the previous lines, and just keep the commands after the below FROM
#it helps to reduce the size of  the image 
FROM openjdk:8-alpine

#Copy the jar from the stage "builder" to the container
COPY --from=builder /app/target/my-app-1.0-SNAPSHOT.jar /opt/app.jar

CMD java -jar /opt/app.jar
