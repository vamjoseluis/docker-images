**Jenkins**

This example creates a Jenkins container and run on 7070 port.

**Steps:**
1. Pull the image
```
$ docker pull jenkins 
```

2. Create a container
```
docker run -d -p 7070:8080 --name jenkins-container jenkins
```

3. Open a browser and got to localhost:7070
- Unlock Jenkins
	- Connect to the container in order to copy the password from /var/jenkins_home/secrets/initialAdminPassword
	```
	$ docker exec -ti jenkins-container bash
	```
	- Print the password
	```
	$ cat /var/jenkins_home/secrets/initialAdminPassword
	```
	- paste the pasword

Done


