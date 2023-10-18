#LAMP STACK IMPLEMENTATIONL(Linux, Apache2, MySQL and Php)


##Prerequisite


signed into my aws console

lunched and instance named it apache2 
server and security setting to port 80

ssh into the instance after i cd into my Dowloads where i hve my keys

![Alt text](images/sshin2apache2-server.jpg)


##STEP1 -INSTALLING APACHE2 WEB SERVER

ran the following commands

sudo apt update

sudo apt install apache2 -y
![Alt text](images/sudoapt-upadate.jpg)
![Alt text](images/apache2-installation.jpg)
![Alt text](images/apache2-installed.jpg)

to cofirm that apache2 is running i ran the systemctl status command

sudo systemctl status apache2

![Alt text](images/apache2-status-confirmed.jpg)



copied the IP address on the browser to confirm if apache2 works

http://<16.16.201.249>:80

![Alt text](images/apache2-works.jpg)


#INSTALLIN MYSQL
##Step2 -installing mysql

ran $ sudo apt install mysql-server

![Alt text](images/apache2-mysqlinstalling.jpg)
![Alt text](images/apache2-mysqlinstalled.jpg)

moved into the mysql enviroment and create data base by running:

$ sudo mysql

$ sudo mysql_secure_installation

$ sudo mysql -p

![Alt text](images/mysql-passwordconfig.jpg)
![Alt text](images/mysqlpsw-changing.jpg)
![Alt text](images/mysqlpsw-changingdonejpg)




#STEP3-INSTALLING PHP


ran:

sudo apt install php libapache2-mod-php php-mysql

'php -v'

![Alt text](images/phpinstallation1.jpg)
![Alt text](images/phpinstallation2.jpg)
![Alt text](images/phpinstallationdone.jpg)



#STEP5 ENABLING PHP ON THE WEBSITE

-i change the file other from index.html to info.php 

-reloaded 

-created and empty file in the projectlamp directory 

-imputed the php valid code or scripts 

-copied the IP address and pasted on a browser to deplay the php configpage


`sudo vim /etc/apache2/mods-enabled/dir.conf`

$ sudo systemctl reload apache2

$ vim /var/www/projectlamp/index.php
![Alt text](images/phpfile-reconfig.jpg)
![Alt text](images/phpfile-reconfig.jpg)
![Alt text](images/php-page.jpg)



##STEP4-CREATING A VIRTUAL HOST

**this was done by mkdir called 'projectlamp'**

-assigned ownership to this directory

-created a file within the directory called 'projectlamp.conf'

-pasted the code and reloaded apache2

-to test that the virtual host works, created and index.html file in the projectlamp directory and copied the hello lamp into it and reloaded and the copied the IP address in the web and it works

-then i edited the index.html file with my own code and reloaded and refresh the web and my webpage came up.

$ sudo mkdir /var/www/projectlamp

$ sudo chown -R $USER:$USER /var/www/projectlamp

$ sudo vi /etc/apache2/sites-available/projectlamp.conf

$ sudo apache2ctl configtest

$ sudo systemctl reload apache2



![Alt text](images/apach2file-edit.jpg)
![Alt text](images/hellolamp-page.jpg)
![Alt text](images/myweb-pageworks.jpg)
















