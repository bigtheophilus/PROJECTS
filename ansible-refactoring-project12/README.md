# ANSIBLE REFACTORING PROJECT DOCUMENTATION

## AIM:the purpose of this project is to improve on the code arragement, readibility and scalabilit of project 11 and creating a path to save all artifact in other to decloud our jenkins server from getting conjested.


## Step1 setting up my server. note that i am continueing the project with my ansible-jenkins server used in project which already has ansible and jenkins running.

### on the home directory a folder called "ansible-config-artifact" was created to save all artifacts and permission was given so that ubuntu can use the folder 

`sudo mkdir ansible-config-artifact`
`chmod -R 0777 /home/ubuntu/ansible-config-antifact`
![Alt text](images/ansible-config-artifact-mkdir.png)

### log into my jenkins web console to install a plugins called "copy artifacts" without restarting jenkins on this path manage jenkins>>plugins>>tab search for "copy artifact"
![Alt text](images/in-jenkins-webconsole-to-install-copy-artifacts.png)
![Alt text](images/copy-artifact-installed.png)

### already have a project called ansible on jenkins so it will act as my upstream project to trigger a downstream project so that whenever i run a build on the project it will triger a buld on the downstream project hence i created a new free style project called save_artifacts to saerve as my downstrem project

### however this folder; save_artifacts was located on a this path /var/lib/jenkins/workspace but i have to move it to the home directory of ubuntu to acchieve te aim.

### configured the save_artifacts project
![Alt text](images/creating-freestyle-project-save_artifactsshow.png)

![Alt text](images/creating-freestyle-project-save_artifacts.png)

![Alt text](images/creating-freestyle-project-save_artifactsdone.png)
![Alt text](images/creating-a-build-step.png)
![Alt text](images/mv-saved-artifacts-into-home-ubuntu-save-artifact-config-path.png)
![Alt text](images/confirmed-build-in-artifacts.png)




# Step2 refactoring by importing other playbooks

### created a new branch called refactor where all my work be done before merging to the main brain. in real time production the refactor branch is the only enviroment where i am permited to make changes and then make a pull request for my code to be checked and approved befor been merged to the main branch which is like the prouction enviroment.

`git checkout refactor`

### touched a new file on my playbook called site.yml

`touch site.yml`

### created a new folder in root of the repository called "static-assignments" and then moved my common.yml file that contain the code for project 11 into this static-assignments folder

`sudo mkdir static-assignments`

`sudo mv common.yml a/nsible-config-mgt/static-assignments`

### then inside site.yml i imported common.yml
![Alt text](images/site.yml-created-inplaybook.png)
![Alt text](images/site.yml-inside.png)
![Alt text](images/static-assignments-folder-created.png)

### so i created another file inside static-assignments folder(because its met to hold all other playbooks) called common-del.yml to carry the codes to delete wireshark that was installed in my server in project11 
### updated the site.yml file with the new file common-del.yml instaed of common.yml and git add . ,git commit -m, git push and merge and on my server cd into ansible-config-mgt on the home diretory and git pull to bring all my changes to the production line and ran the playbook against dev (the file with the target server IPs)

`touch common-del.yml`
![Alt text](images/connect-server-via-ssh-A.png)
![Alt text](images/playbook-del-ran-sucessfully.png)

![Alt text](images/test-wireshark-del.png)


# Step3 configure UAT wedservers with a role webserver

## i already have two reheart servers from project 11 so i did not need to provision new ones so  onle copy their private IPs into my inventory/uat.yml

### on my local system on the ansible-config-mg path, i made a directory called roles and cd into it and because my system is a windows system and i dont have ansible installed in it , i therefore install ubuntu-wsl so i can install ansible in my local system in other to run the 'ansible-galaxy init webserver' command

## to install ubuntu-wsl ran  `wsl --intsall`  on my sytem powershell enviroment as admin
## and restarted my local system

### the `ansible-galaxy init webserver` created under the roles directories with it depencies folders/files

### configured my `sudo vi /etc/ansible/ansible.cfg`

### to state the path of the roles inventory and disable ssh_key_checking

### on the role websever path, there is a folder called task with a file caled main.yml which i used o write the logic or code to install apache and fork the tooling file. i have forked the tooling repo to my git hub account in an earlier project

![Alt text](images/roles-dependencies.png)

![Alt text](images/roles-dependencies2.png)

![Alt text](images/roles-dependencies-successfull.png)
![Alt text](images/configured-ansible.cfg.png)
![Alt text](images/main.yml-coded.png)

![Alt text](images/uat.yml-servers-updated.png)
![Alt text](images/uat-webservers.yml-coded.png)

all git push and pull was succefully don and the playbook ran successfully 
![Alt text](images/final-playbook-run.png)

![Alt text](images/final-playbook-run-wirked.png)


# Step 5 confirme if the tooling interface shows if the public ip of my servers are ran on the web/index.php
![Alt text](images/tooling-interface-web1.png)
![Alt text](images/tooling-interface-web2.png)
