FROM centos

LABEL version=latest
LABEL description="This is an example of a docker image, which  contains centos, apache and a simple html project"
LABEL vendor="tuxpuck"

#to install httpd
#-y means yeas, it is due yum install will ask if we want to install it
RUN yum install httpd -y

#to move the current work dir to a new path (after that, you must use . to indicate the current path)
WORKDIR /var/www/html

#copy folder project to /var/html
#you can use ADD instead, but ADD also can pull files from a URL
COPY business .

#to add environment variables
ENV envValue dev
##just print the envValue in test.html
RUN echo "<h3>Please find below the information of this image</h3>" > ./info.html
RUN echo "<br><b>envValue:</b> $envValue" >> ./info.html

#to expose an specific port, we can use EXPOSE
#EXPOSE 8080

RUN echo "<br><b>currentUser:</b> $(whoami)" >> ./info.html
RUN useradd tuxpuck
#to set a specific user
USER tuxpuck
RUN echo "<br><b> currentUser:</b> $(whoami)" >> /tmp/info.html
USER root
RUN cat /tmp/info.html >> ./info.html

#to run apache in foreground
CMD apachectl -DFOREGROUND

