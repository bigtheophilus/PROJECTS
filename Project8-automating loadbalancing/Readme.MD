# AUTOMATING LOAD BALANCING THROUGH SHELL SCRIPTING

# Step1:provision two ubuntu based servers nameed server1 amd server2.

![Alt text](IMAGE/provisioned-twowebserveres.png)

## set the inbound rules to listen at port 8000 everywher
![Alt text](IMAGE/set-inboundrules.png)

## ssh into the servers via the gitbash channel

## created a file called install.sh and pasted the codes

![Alt text](IMAGE/file-created-with-code.png)

![Alt text](IMAGE/file-created-with-code.png2.png)

## saved and changed mode to make the file executable;

`sudo nano install.sh`

`sudo chmod+x install.sh`

![Alt text](IMAGE/chmod-and-execute-file.png)

![Alt text](IMAGE/chmod-and-execute-file.png2.png)


## ran and executed the file succefully:

./install.sh 16.170.232.173

./install.sh  51.20.6.179

![Alt text](IMAGE/file-executed.png)

![Alt text](IMAGE/file-executed2.png)

## pasted the public IP of the server on the web to check if it works

![Alt text](IMAGE/server1-page-success.png)
![Alt text](IMAGE/server2-page-success.png)


# Step2 setting up the Nginx load balancer serever as follows:

## provision a server name Nginx-load-balancer
![Alt text](IMAGE/provisioned-nginx-instance.png)

## sett the inbound rules to port 80 everywher
![Alt text](IMAGE/nginx-inbound-rule-set.png)

## ssh into the server via git bash CLI

## created a file called 'nginx.sh' and pasted the code

`sudo nano nginx.sh`

![Alt text](IMAGE/nginx-file-created.png)

## file saved and changed mode to make it executable

`sudo chmod +x nginx.sh`
![Alt text](IMAGE/nginx-chmod-execute.png)


## executed the nginx.sh file with its public IP, server1 and server2 public IPs

`./nginx.sh 13.48.10.95 16.170.232.173 51.20.6.179`

![Alt text](IMAGE/nginx-executed-success.png)

## pasted the nginx IP on the web and it didplayed the server one page and when refreeshed server2 and so on . this showed that nginx worked succesfully as a load balacer to distribute the traffic 

![Alt text](IMAGE/nginx-displayed-server1IP.png)

![Alt text](IMAGE/nginx-displayed-server2IP.png)
