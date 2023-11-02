# Implementing Wordpess Website With LVM Storage Management


# STEP 1

## lunched a redheart webserver
## created volumes and attached the volumes to the server disk
## ssh into the server and created partitions for each of the ceated volumes

`sudo gdisk /dev/volume-name`

![Alt text](Images/lunched-instance.png)
![Alt text](Images/attached-volumes.png)
![Alt text](Images/attached-volumes2ok.png)

![Alt text](Images/ssh-into-server.png)
![Alt text](Images/create-partition-disk1.png)
![Alt text](Images/create-partition-disk2.png)
![Alt text](Images/create-partition-disk3.png)


# STEP2 

## installed LVM2 by 

`sudo yum install LVM2 -y` 

![Alt text](Images/installing-LVM2.png)
![Alt text](Images/installing-LVM2-omplete.png)

## used the 'pvcreate' utility to create physical volumes for each of the attached volumes and confirm the created physical volumes 

`sudo pvcreate /dev/volume-name`

`sudo pvs`
![Alt text](Images/PV&VG-created.png)

## used the 'vgcreate' to add all the 3 physical volumes to a group called webdata-vg

`sudo vgcreate webdata-vg /dev/pv1/pv2/pv3`
![Alt text](Images/PV&VG-created.png)

## verified using 

`sudo vgs`

## used the 'lvcreate' utility to create two logical volumes one for apps "Apps.lv and the other for logs "log-lv" and verify the succesful creation of these lv

`sudo lvcreate -n apps-lv -L 14G webdata-vg`
`sudo lvcreate -n logs-lv -L 14G webdata-vg`
`sudo lvs`
![Alt text](Images/2-logical-volume-created.png)


## verified the entire setup

`sudo vgdisplay -v #view complete setup - VG, PV, and LV`
`sudo lsblk` 
![Alt text](Images/confirmed-entire-setup1.png)

## formated the lv with mkfs.ext4 utility

`sudo mkfs -t ext4 /dev/webdata-vg/apps-lv`
`sudo mkfs -t ext4 /dev/webdata-vg/logs-lv`
![Alt text](Images/file-edited.png)


# STEP3

## Created the /var/ directory and the /home/ directory and then mount the app-lv on the /var/www/html directory and the logs-lv on the /var/log directory

`sudo mkdir -p /var/www/html`
`sudo mkdir -p /home/recovery/logs`
sudo mount /dev/webdata-vg/apps-lv /var/www/html/
sudo rsync -av /var/log/. /home/recovery/logs/
sudo mount /dev/webdata-vg/logs-lv /var/log

![Alt text](Images/making-var$home-directories.png)

![Alt text](Images/mounted-vg-the-var-diretory.png)

## confirm the uuid
![Alt text](Images/confirming-UUID-VG$LV.png)

 ## updated the file
![Alt text](Images/file-edited.png)
![Alt text](Images/entire-setup.png)


# STEP4

## installed wordpress on the server, wget httpd and all its dependencies

`sudo yum update -y`
`sudo yum install wget httpd php php-myslqnd php-fpm php-json`
`sudo systemctl enable httpd`
`sudo systemctl start httpd`
![Alt text](Images/installing-wget-apache-and-dependencies.png)
![Alt text](Images/installing-wget-apache-and-dependenciesok.png)
![Alt text](Images/enabled&start-httpd.png)

## installed PHP and its dependencies then download wordpress and copy to /var/www/html directory.

NOte:this was done by writing a script and running to carry out the command at once
![Alt text](Images/installingapache-dependencies.png)
![Alt text](Images/installingapache-dependenciesok.png)
![Alt text](Images/downloadwordpress&copy2-var-directory.png)
![Alt text](Images/downloadwordpress&copy2-var-directoryok.png)

## config SELinux-policies
![Alt text](Images/configured-SElinux-policies.png)

## installed mysql-client in the websever in order to help communicate with my DB-webserver

`sudo yum install mysql -y`


# ON THE DATABASE SERVER THE STEPS WERE REPEATED TO CREATE VOLUMES, ATTACHED VOLUMES PARTITION VOLUMES CREATE PHYSICAL VOLUMS AND GROUP THEM IN A GROUPVOLUME AND INSTALL LVM2 AND CREATE TWO LOGICAL VOLUMES THIS TIME THE "APP-LV" now "DB-LV" MOUNTED ON THE /db/ DIRECTORY CREATED AS AGAINST THE /var/www/html DIRECTORY.
## installed mysql on the db-server and configureed to listen @ port 3306 created a user called 'myuser' ans password called 'mypass'
![Alt text](Images/DB-instance-lunched.png)
![Alt text](Images/DBvolumes-created.png)
![Alt text](Images/attaching-volumes-DB.png)
![Alt text](Images/db-volumes-partioning.png)
![Alt text](Images/db-volumes-partioningdone.png)
![Alt text](Images/physicalV-created-on-DB.png)
![Alt text](Images/LV-created-DB.png)
![Alt text](Images/VG-created4-pv-on-DB.png)
![Alt text](Images/mkdir-db&mounting-volumes1.png)
![Alt text](Images/mkdir-db&mounting-volumes2.png)
![Alt text](Images/lvm2-installed-on-DB.png)
![Alt text](Images/confirm-uuid-DB.png)
![Alt text](Images/confirm-entire-setup-DB.png)

![Alt text](Images/installed-db-server-on-DB.png)

![Alt text](Images/configuredDB-createDB-showDB.png)

![Alt text](Images/formating-db-filesystem.png)

## connected to my DB-server via the mysql-client on the webserver and showdatabases
![Alt text](Images/connected-to-mydatabase-server.png)

## configured the wp-config.php on the /var/www/html/wordpress directory and imputed my DB credentials
![Alt text](Images/configured-wp-config.php.png)

## pasted the public_IP of my webserver on my browser to populate the wordpress installation-page and imputed datas and require and continued to the welcome page.
![Alt text](Images/wordpress-page-up.png)
![Alt text](Images/wordpress-dash-bored.png)
![Alt text](Images/welcome-to-wordpres-page.png)

















