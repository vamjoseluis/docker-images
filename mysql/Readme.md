**How to create a MySQL container**

In this example we will create a container with the below specifications
- MySQL:
	- Database name: test
	- User: test-user
	- Password: userSecret
	- Root password: superSecret

- Container:
	- Name: mysql-db
	- Port:3306
	- With Image: mysql:latest


**Step 1. Pull an image**
```
#pulling latest image
$ docker pull mysql:latest
```

**Step 2. Create a container**
```
$ docker run -d -p 3306:3306 --name mysql-db  -e "MYSQL_ROOT_PASSWORD=superSecret" -e "MYSQL_DATABASE=test" -e "MYSQL_USER=test-user" -e "MYSQL_PASSWORD=userSecret" mysql:latest
```

**How to connect**
- As root user
```
$ mysql -u root -psuperSecret -h 127.0.0.1 --port 3306
```
- As test-user
```
$ mysql -u test-user -puserSecret -h 127.0.0.1 --port 3306
```


**Notes**
- Be aware that you have already insalled ***MySQL client***
- Be aware that you client is compatible with the DB version
- This was tested with MYSQL 8.0.27 and Client 8.0.23