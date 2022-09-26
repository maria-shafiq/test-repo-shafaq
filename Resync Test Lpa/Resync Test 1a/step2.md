---
title: Docker is ephemeral

---
Let's start by running a MariaDB database container:

{{ execute }}
```
docker run \
--name mariadb \
-e MYSQL_ROOT_PASSWORD=p455w0rd \
-d mariadb
```
{{ /execute }}

Usually MariaDB stores the database in `/var/lib/mysql`.  Let's now check the filesystem of the container. We are concerned about MariaDB data directory:

{{ execute }}
```
docker exec -it mariadb ls /var/lib/mysql
```
{{ /execute }}

When you are developing an application with MariaDB as your database, you will usually store and update data rows and columns from your database tables. All of the updates are stored inside your container. As said before, the problem is that containers when are destroyed (voluntarily or accidentally), all data will be wiped unlike when you run MariaDB in a VM: 

When you run MariaDB on your VM, when you stop the database service, your data is preserved on your localhost.