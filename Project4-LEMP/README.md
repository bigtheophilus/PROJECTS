#WEB STACK IMPLEMENTATION (LEMP)

##Prerequisites

-log into my AWS account lunched an instance called "Nginx-server" with open port80 securty settings

-ssh to connect to the sever after cd into my Downloads on my bash interface
![Alt text](<images/lunch instance.jpg>)
![Alt text](<images/ssh into instance.jpg>)


#STEP1 INSTALLING THE NGINX WEB SERVER

##comand ran.

`sudo apt update`

`sudo apt install nginx`

`sudo systemctl status nginx`
![Alt text](images/nginxinstallation-1.jpg)
![Alt text](images/nginxinstalledjpg.jpg)
![Alt text](images/nginxinstalled-works.jpg)
![Alt text](images/NGINX-RUNNI.jpg)

###accessing it in ubutu shell, i ran the curl command

`curl http://localhost:80`

`http://http://13.53.159.210:80`
![Alt text](images/curl-nginx.jpg)
![Alt text](images/nginx-pageworks.jpg)


#STEP2-INSTALLING MYSQL

 `sudo apt install mysql-server`

`sudo mysql`

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

![Alt text](images/mysql-installation1.jpg)
![Alt text](images/mysql-installation2.jpg)
![Alt text](images/mysqlinstallation-done.jpg)


`sudo mysql_secure_installation`

`sudo mysql -p`

`mysql> exit`
![Alt text](images/mysqlconfig-1.jpg)
![Alt text](images/mysqlconfig-2.jpg)
![Alt text](images/mysqlconfig-done.jpg)


#STEP3-INSTALLING PHP

`sudo apt install php-fpm php-mysql`

![Alt text](images/Nginx-phpinstallation1.jpg)
![Alt text](images/Nginx-phpinstallation2.jpg)


##STEP4/5-CONFIGURING NGINX TO USE PHP PROCESSOR

`sudo mkdir /var/www/projectLEMP`

`sudo chown -R $USER:$USER /var/www/projectLEMP`

`sudo nano /etc/nginx/sites-available/projectLEMP`

`sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`

`sudo nginx -t`

`sudo unlink /etc/nginx/sites-enabled/default`

`sudo systemctl reload nginx`

![Alt text](images/NGINX-PHPconfig1.jpg)
![Alt text](images/NGINX-PHPconfig2.jpg)
![Alt text](images/NGINX-PHPconfig3.jpg)
![Alt text](images/NGINX-PHPconfig4.jpg)
![Alt text](images/nginex-hellopageworks.jpg)
![Alt text](images/nginx-phppageworks.jpg)


#STEP6-CREATING DATABASE USING MYSQL


`sudo mysql`

`mysql> CREATE DATABASE `example_database`;`

`mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

`mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';`

`mysql> exit`

`mysql -u example_user -p`

`mysql> SHOW DATABASES;`

`mysql> exit`
![Alt text](images/Mysqldatabase-works1.jpg)
![Alt text](images/Mysqldatabase-works3.jpg)
![Alt text](images/Mysqldatabase-works2.jpg)
![Alt text](images/Mysqldatabase-works.jpg)







please i am open for corrections

