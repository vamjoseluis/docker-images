FROM maven:3.5-alpine as builder

COPY app /app

RUN cd /app && mvn package

#With this FROM we are going to discar the previous lines, and just keep the commands after the below FROM
#it helps to reduce the size of the image 
FROM openjdk:8-alpine

COPY --from=builder /app/target/my-app-1.0-SNAPSHOT.jar /opt/app.jar

CMD java -jar /opt/app.jar
