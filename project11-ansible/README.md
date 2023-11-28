
# ANSIBLE-AUTOMATE PROJECTION

## AIM
## the purpose of this project is to automate the management of servers such as webservers, db-servers, LB-servers from a single server called the controller or bastion Host or Jumper server via the use of ansible playbook 

# Step1 PROVISIONING SERVERS AND INSTALLING APPLICATIONS 
## provisioned an ec2 of ubuntu and named it ansible-jenkins opened port 22 and 8080 as ansible and jenkins were install in it.....this served as the controller.
## configure jenkins for a job on git repo
![Alt text](images/hostservers-created.png)
![Alt text](images/securitygrp-setting-jenkins.png)
![Alt text](<images/ansible installed.png>)
![Alt text](images/jenkins-instalaton.png)
![Alt text](images/jenkins-fully-installed.png)
![Alt text](images/jenkins-login-interface.png)
![Alt text](images/jenkins-config-gitsource.png)
![Alt text](images/confirm-files-reflecr-inserver.png)
![Alt text](images/freestyle-project-succesful-jenkins.png)


## created a repo on github named ansible-config-mgt and added a webhook with the url of my jenkins application added to it in other to beable to connect and triger saving of my artifacts
![Alt text](images/repo-created.png)
![Alt text](images/webhook-created.png)
![Alt text](images/confirmed-built-playbook&inventory.png)
![Alt text](images/readme-file-created-vscode.png)


# Step2 SETTING UP MY VSCODE WORKSPACE

## git clone my repo to my vscode workspace

`git clone https://github.com/bigtheophilus/ansible-config-mgt`
![Alt text](images/gitcloned-repo-to-vscode.png)


# Step3 BEGIN ANSIBLE DEVELOPMENT

## created new branch named dev

## created new directories named playbook and inventory on the repo via vscode

## within the playbook a file name common.yml was crated and within inventory the following file was created:dev.yml, staging.yml prod.yml uat.yml
![Alt text](images/created-new-branch.png)

![Alt text](images/created-playbook$inventory-directory.png)
![Alt text](images/created-files-inside-inventory$playbook.png)


# Step4 CONFIGURATIONS

## all the host servers to be managed private ips where grouped and saved in the inventory/dev.yml file
![Alt text](images/hostservers-created-ipsaved.png)

## connected the host severs via the ssh agent from the bastion server
![Alt text](images/connect2-controllervia-ssh-A.png)
![Alt text](images/sshconnected2-targeted-host.png)
![Alt text](images/host_key_checkinh_f-cfgfile.png)

# Step5 CREATING PLAYBOOK

## copied the codes in the the playbook/common.yml file for instruction and git add. commit and push it then merge it to the main branch and confirmed the artifacts are saved in jenkins

![Alt text](images/codes-into-common.yml.png)
![Alt text](images/switched-to-dev-branch.png)
![Alt text](images/git-merge-interface.png)
![Alt text](images/git-interface.png)
![Alt text](images/artifactssaved-injenkins.png)
![Alt text](images/vscode-interface-workflow.png)


# Step6 RUN FIRST PLAYBOOK

## Ran the playbook but first git clone my repo into my bastion server then cd into the andsible-config-mgt directory and git pull to bringdown the lates changes in my repo into the server and the ran the playbook successfully. confirmed wireshark installed

`ansible-playbook -i inventory/dev.yml playbook/common.yml`

![Alt text](images/gitclonedrepo-to-controller-server.png)
![Alt text](images/git-clone-pull-intoserevr.png)
![Alt text](images/cd-into-ansible-config-mgt.png)
![Alt text](images/ran-playbook-succeful.png)
![Alt text](images/ran-playbook-succeful.png2.png)
![Alt text](images/confirmed-wireshark-installed-on-targets.png)


# Step7 REPEAT PLAYBOOK WITH DIFFERENT CODES

## i repeated the playbook run by making a folder named 'ansible-testing' on the home directory and a file named 'testing' inside the directory and confirmed this path on the target hostserver
![Alt text](images/repeat-ranplaybook4mkdr-verified-on-hostserver.png)
![Alt text](images/repeat-ranplaybook4touch-verified-on-hostserver.png)



### i must say it was overwhelming but it was a success