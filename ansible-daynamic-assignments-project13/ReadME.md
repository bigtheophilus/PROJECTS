
# ANSIBLE DYNAMIC ASSIGNMENT(include) PROJECT 13

## This project is aimed at achieving configuration with the include module, its a continuation of project 11 and 12. In project 12 we explored static assignment where we used the export module to ahieve the configuration but in this dynamic assignment include module is used which is the major difference between static and dynamic assignments.
# import =static assignment
# include =dynamic asignment

# in export (static assignments) when executing site.yml,playbook, ansible will process all the playbooks refereced during the time it is parsing the statements. what this means is that during the actual execution, if any statement changes, such statements will not be considered, hence its static

# while include (dynamic assignments) all statemets are processed only during execution of thr playbook. that is any changes tothe statements encountered during execution will be used.

# NOTE:
# static assigments are more reliable and stable than dynamic assignments hence they are most recommended. however dynamic assignments can be used for enviroment specific variables.

## Step one created a dynamic assignment branch and new folder called dynamic assignment and a file called env-vars.yml

![Alt text](imagesdynami-assignments-branche-created.png)

![Alt text](imagesdynamic-assignments-folder-env-vars-file.png)

![Alt text](images/env-vars-folder&env-files-created.png)

![Alt text](images/tree-structure-verified.png)

# updated site.yml
![Alt text](images/site.yml-updated.png)

# used the Ansible galaxy community to install the roles necessary, mysql etc
## after editing the roles changes where committied to github acct and branch merged to the main and pull to the production server or enviroment and the playbook was ran inventory/dev.yml aganst playbook/site.yml
![Alt text](images/ansible-galaxy-mysql-in-role.png)
![Alt text](images/code-pasted-n-env-var-file.png)
![Alt text](images/Config-main.yml-for-database.png)
![Alt text](images/editing-role-configuration-for-mysql.png)
![Alt text](images/git-add-from-server-to-github-repo.png)
![Alt text](images/git-push-dynamic-assignments-to-github.png)
![Alt text](images/githubview.png)
![Alt text](images/request-for-PR-ongithub-role-feature-branch.png)

![Alt text](images/gitpush-from-server-togithub-repo.png)
![Alt text](images/inventory-dev.yml-against-playbook-site.yml.png)
![Alt text](images/inventory-dev.yml-against-playbook-site.yml2.png)
![Alt text](images/inventory-dev.yml-against-playbook-site.yml3.png)
![Alt text](images/inventory-dev.yml-against-playbook-site.yml4.png)

# setting nginx and apache loadbalancers

## on defaults/main new configuration setting made and on static assignments folrders created file for apache and nginx and then ran the play book to install and configure nginx as a load balancer and repeat the same for apache
![Alt text](images/play-run-after-error-done.png)
![Alt text](images/play-run-after-error.png)
![Alt text](images/confirmed-nginx-installed-on-server.png)


Thanks!












