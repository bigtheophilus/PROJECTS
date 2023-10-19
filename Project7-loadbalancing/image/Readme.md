# SETTING UP A BASIC LOAD BALANCER

## Step1 provisioning 3 instances 
### two have apache2 installed in them and the other Nginx

### port 8000 is open on the apache2 servers and set to allow traffic everywhere, while port 80 is open on the nginx server.....
![Alt text](instances-lunched.png)
![Alt text](setting-boundrules1.png)
![Alt text](setting-boundrules-nginx.png)


## Step2 Install apache2 into the servers

### ssh into the servers to connect on the command line

### update and install apache2

### confirm that apache2 is active and running in the two servers.......

`sudo apt update -y &&  sudo apt install apache2 -y`

`sudo systemctl status apache2`

![Alt text](ssh-into-apache2-server1.png)
![Alt text](ssh-into-apache2-server1done.png)
![Alt text](ssh-into-apache2-server2.png)
![Alt text](ssh-into-apache2-server2done.png)
![Alt text](installingapache2-onserver1.png)
![Alt text](installingapache2-onserver1done.png)
![Alt text](installingapache2-onserver2.png)
![Alt text](installingapache2-onserver2done.png)
![Alt text](apache2-confirmed-running&active-on-both-servers.png)


## Step3 Apache2 configuration

### configured apache2 to server content on port 8000. this was done by adding 8000 to the already existen listen port 80

`sudo nano /etc/apache2/ports.conf` 
![Alt text](<added port8000-configuration.png>)

### effect the change on the default file on site-available

`sudo nano /etc/apache2/sites-available/000-default.conf`
![Alt text](etc-configuration8000.png)

### saved changes and restarted apache2 server

`sudo systemctl restart apache2`
![Alt text](commands-till-restartservers.png)

### created a new file index.html amd posted the code in it 'welcome to my EC2 public ip'.

`sudo nano index.html`
![Alt text](creating-a-file.html.png) 

### changed the file ownership

`sudo chown www-data:www-data ./index.html`
![Alt text](commands-till-restartservers.png)

### copy cotent into the default file on html dirrectory to overide it

`sudo cp -f ./index.html /var/www/html/index.html`
![Alt text](commands-till-restartservers.png)

### then restarted apache2 on bothe servers

`sudo systemctl restart apache2`
![Alt text](commands-till-restartservers.png)

### paste the public IP of my servers on the tab to desplay my content page
![Alt text](welcome-page-.png)

![Alt text](welcome-page2.png)


## Step4 working on the load balancer

### ssh into the server
![Alt text](ssh-into-loade-balancer.png)
![Alt text](ssh-into-loade-balancer-done.png)

### update and install nginx 

`sudo apt update -y && sudo apt install nginx -y`
![Alt text](installin-nginx-in-load-balancer.png)
![Alt text](installin-nginx-in-load-balancer-done.png)


### verified that nginx is active and running

`sudo systemctl status nginx`
![Alt text](<confirm Nginx-is-active&running.png>)


### configure nginx by injecting the public IPs of my apache2 servers into the upstream backed block, then that of my load balancer as well.

`sudo nano /etc/nginx/conf.d/loadbalancer.conf`
![Alt text](configuring-load-balancer.png)

### tested and restarted nginx load balance

`sudo nginx -t`

`sudo systemctl restart nginx`
![Alt text](testing-config-ok.png)

### papsted the public IP of my load balance on the tab and desplayed my servers web pages after reloading
![Alt text](load-balacer-webpage1.png)
![Alt text](loadbalancer-webpage2.png)


NOTE: initially i had a 504 gate way error and i discovered it was because i lunched the tree instance with same security group. This affected the inbound rules editng. however i had to delete the nginx instance and lunched another with a new security group. 

