# DEVOPS TOOLING WEBSITE SOLUTION
### in this project a tooling website is designed to house all the commonly used tools in Devops using the following components;
## AWS infrastructure
## RHEL-8.6 based webserver
## ubuntu 20.04 base MYSQL database server
## RHEL-8.6 based Network file system as storage server
## PHP programming language
## repo from git with the codes



# NFS in this project serves as the backend file storage, therefore followed the below steps to set up the server, attach volumes to increase its capacity and set it up to communicate with the webservers

## step 1 provisioned an EC2 RHEL-8.6 NFS server and named it 'nfs-server'
![Alt text](images/nfs-server-lunched.png)

## step 2 created 3 volumes and attached the volumes to nfs-server main disk
![Alt text](images/3volumes-created.png)
![Alt text](images/3volumes-attached.png)

## ssh into the server to confirm attched disk and configure them
![Alt text](images/ssh&confirm-disk.png)

## disk where partitioned using  'gdisk' utility

`sudo dev/nvme1n1`

`sudo /dev/nvme2n1`

`sudo /dev/nvme3n1`

![Alt text](images/diskpart1-created.png)
![Alt text](images/diskpart2-created.png)
![Alt text](images/diskpart3-created.png)

## install the lvm2 package using;
`sudo yum install lvm2 -y`

![Alt text](images/lvm2-installed.png)
![Alt text](images/lvmdiskscan.png)

## using the pvcreate utility to create physical volumes; vg utility to group volume(webdata) the physical volumes greated; lv utility to create 3 logical volumes named as apps, logs. opt

`sudo pvcreate /dev/nvme1n1p1`

`sudo pvcreate /dev/nvme2n1p1`

`sudo pvcreate /dev/nvme3n1p1`

`sudo vgcreate webdata-vg /dev/nvme1n1p1 /dev/nvme2n1p1 /dev/nvme3n1p1`

`sudo lvcreate -n lv-apps -L 9G webdata-vg`

`sudo lvcreate -n lv-logs -L 9G webdata-vg`

`sudo lvcreate -n lv-opt -L 9G webdata-vg`


![Alt text](images/pv-vg-lv-created&conformed.png)


## lv file system formated to nfs using 'mkfs' utility;

`sudo mkfs -t xfs /dev/webdata-vg/lv-apps`

`sudo mkfs -t xfs /dev/webdata-vg/lv-logs`

`sudo mkfs -t xfs /dev/webdata-vg/lv-opt`
![Alt text](images/formating-lv-filesystem.png)

## created directory tp moun the lvs and mount the lvs on the directory created;

`sudo mkdir /mnt/apps`

`sudo mkdir /mnt/logs`

`sudo mkdir /mnt/opt`

`sudo mount /dev/webdata-vg/lv-apps /mnt/apps`

`sudo mount /dev/webdata-vg/lv-logs /mnt/logs`

`sudo mount /dev/webdata-vg/lv-opt /mnt/otp`

![Alt text](images/formating-lv-filesystem&dircreated&mounted.png)


## NFS util install in the server and changed inbound rules

`sudo yum -y update`

`sudo yum install nfs-utils -y`

`sudo systemctl start nfs-server.service`

`sudo systemctl enable nfs-server.service`

`sudo systemctl status nfs-server.service`
![Alt text](images/nfs-updated&utils-installed.png)
![Alt text](images/nfs-inbound-rules-changed.png)

### give permission to this directory. note that this permisssion are automated in apache for /var/www/html directoy

`sudo chown -R nobody: /mnt/apps`

`sudo chown -R nobody: /mnt/logs`

`sudo chown -R nobody: /mnt/opt`

`sudo chmod -R 777 /mnt/apps`

`sudo chmod -R 777 /mnt/logs`

`sudo chmod -R 777 /mnt/opt`

`sudo systemctl restart nfs-server.service`
![Alt text](images/permission-nfs.png)

## configure access to clients into NFS using the server CIDR(172.31.16.0/20)

`sudo vi /etc/exports`

/mnt/apps 172.31.16.0/20(rw,sync,no_all_squash,no_root_squash)

/mnt/logs 172.31.16.0/20(rw,sync,no_all_squash,no_root_squash)

/mnt/opt 172.31.16.0/20(rw,sync,no_all_squash,no_root_squash)

`sudo exportfs -arv`

![Alt text](images/exported-nfs.png)


# lunched a database server and ssh into it installed mysql-server and configured withe nfs CIDR (172.31.16.0/20) 
`create database called tooling`

`create user called webaccess and give it a password`

`grant all permission on tooling to webaccess`

`show databases`

`made biding site accessble on mysql(0.0.0.0)` 

![Alt text](images/db-server-lunched.png)
![Alt text](images/mysql-installed-onDB.png)
![Alt text](images/DB-configured.png)
![Alt text](images/Db-etcconfig-done.pnghm.png)
![Alt text](images/Db-etcconfig-done.png)

![Alt text](images/DB-configured.png)

# prepared the first webserver
## lunched the server and open port 80
## install NFS-client in it
## make a /var/www directory to mount the /mnt/apps in the NFS-server
## mount and confirmed it persist 

`sudo yum install nfs-utils nfs4-acl-tools -y`

`sudo mkdir /var/www`

`sudo mount -t nfs -o rw,nosuid 172.31.30.81:/mnt/apps /var/www` (private ip of the NFS-server)

`sudo vi /etc/fstab`
![Alt text](images/webserver1-lunched.png)
![Alt text](images/webserver1-installed-nfs-utils.png)
![Alt text](images/wedserver1-confirmed-mount.png)

## installed httpd and php and their dependencies on webserver1 and configured it.

`sudo yum install httpd -y`

`sudo systemctl enable httpd`

`sudo systemctl start httpd`

`sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`

`sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`

`sudo dnf module reset php`

`sudo dnf module enable php:remi-7.4`

`sudo dnf install php php-opcache php-gd php-curl php-mysqlnd`

`sudo systemctl start php-fpm`

`sudo systemctl enable php-fpm`

`sudo setsebool -P httpd_execmem 1`

![Alt text](images/webserver1-httpd-install.png)
![Alt text](images/webserver1-httpd-enabled.png)
![Alt text](images/webserver1-remirepo-installed.png)

![Alt text](images/webserver-httpd-depencies-installed.png)
![Alt text](images/webserver-httpd-depencies-installed2.png)

## made a test.txt file snd confirm it refleted on my NFS-server
![Alt text](images/confirming-testfiles-copied-on-nfs.png)

## located the log directory on httpd(apach) found on //var/log/httpd and mount /mnt/logs on it.
![Alt text](images/mounted-log-savedwebserver1.png)

## installed git and cloned the code repo from darey.io github account to bring down to my server the tooling code in the /var/www/html path disabled selinux 

`sudo yum install git -y`
![Alt text](images/gitconformed-installed-webserver1.png)

git clone 
![Alt text](images/funkdown-repo-webserver1.png)

`sudo setenforce 0`
![Alt text](images/linuxSE-settings.png)
![Alt text](images/linux-disabled-wedserver1.png)

## cd into the location of the tooling folder in my server and applied the tooling-db.sql script to my database and also update the webserver configuration on /var/www/html/functions.php to connecte to my database
![Alt text](images/step10-config.png)
![Alt text](images/db-tooling-cp-tooling-db.sql.png)

## theafter restarting my server and copied the public ip into my browser follow by the path of the tooling directory code file which my case was /html/index.php

![Alt text](images/tooling-login-interface.png)
![Alt text](images/tooling-interface.png)
![Alt text](images/tooling-interface-complete.png)

# it is neccesary to note that along the line of this project i made a mistake during the configuration of my database which was later corrected and effected.

## procedures was also repeated for two other servers and succefully displayed the tooling app interface.