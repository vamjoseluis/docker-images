**Volumenes**
If the container is eliminated, the image will keep the information. It means when the container is created again, the information will be there.

**Host**
It storages the information in the folder specified. 

**Anonymous**
We don't define a folder but there will be a random folder where the container storages the information.

**Named Volumenes**
We create but we don't define the folder and the folders are managed by docker.


**Here is a use case for MySQL**
Accordingly with the MySQL's docs, it storage the information into /var/lib/mysql, so in this example we will persist this folder.

- Define the folder that is gonna keep the information in hour host (for instance I'm gonna use this folder on my machine /Users/myuser/mysql-docker-test).
```sh
$ docker run -d -p 3306:3306 --name mysql-volume-host  -e "MYSQL_ROOT_PASSWORD=superSecret" -v /Users/myuser/mysql-docker-test:/var/lib/mysql mysql:latest

```

- Connect to the DB
```sh
mysql -u root -h 127.0.0.1 -psuperSecret
```

- See the databases available in there
```sh
mysql> show databases; 
```
There will be the below DBs
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
```

- Create some databases
```
mysql>create database mydb1;
mysql>create database mydb2;
mysql>create database mydb3;

```

- check the host folder(/Users/myuser/mysql-docker-test), there you will find:
```
mydb1
mydb2
mydb3
```

- Delete the container
```sh
$ docker rm -fv mysql-volume-host
```

- Create again the image
```sh
$ docker run -d -p 3306:3306 --name mysql-volume-host  -e "MYSQL_ROOT_PASSWORD=superSecret" -v /Users/myuser/mysql-docker-test:/var/lib/mysql mysql:latest
```
- Connect to the DB
```sh
$ mysql -u root -h 127.0.0.1 -psuperSecret
```

- Check tha databases availabe inthere
```sh
mysql> show databases;
```

You should see the DBs you created(db1, db2, db3) before you deleted the container
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mydb1              |
| mydb2              |
| mydb3              |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
```

**Anonymous**
- Delete the previous mysql container
```sh
$ docker rm -fv mysql-volume-host
```

- Create the container without specifying the folder host
```sh
$ docker run -d -p 3306:3306 --name mysql-volume-anonymous  -e "MYSQL_ROOT_PASSWORD=superSecret" -v /var/lib/mysql mysql:latest
```

- Check where the volume has been mounted
```sh
$ docker inspect mysql-volume-anonymous
```

Look for the Mounts.Source property

If the volumen is mounted as anonymous, then if you delete the container with:
```sh
$ docker rm -fv mysql
```
The volume is going to be deleted as well.


**Named volume**

