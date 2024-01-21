# DOCUMENTATION ON ELK STACK INSTALLATIONS

## step 1 

## lunched an ubuntu ec2 instance with a 100g ram and t3*2large, ssh into the instance and updated the instnce 

## knowing that the elasticstack are not located on the ubuntu directory, the key to their residing directory was added and the ditretory added.

    `sudo apt update`

`curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch |sudo gpg --dearmor -o /usr/share/keyrings/elastic.gpg`

`echo "deb [signed-by=/usr/share/keyrings/elastic.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list`

`sudo apt update`

## then now installed elastic search

sudo apt install elasticsearch

sudo nano /etc/elasticsearch/elasticsearch.yml

## in the elasticsearch.yml file uncomment the network.host line and change the value to 'localhost'

## restart and enable elasticsearch

sudo systemctl start elasticsearch

sudo systemctl enable elasticsearch

## to confirm its running, 

curl -X GET "localhost:9200"


# step 2 Installed kibana.
## kibana is a web interface for searching and visualizing logs
## because the repo is already added just proceded to install kibana.

sudo apt install kibana

sudo systemctl enable kibana

sudo systemctl start kibana

### Note kibana is only configured to listen on localhost nginx was used as a reverse proxy to direct users traffic to kibana in other to shed it from users hacking.

### created a password for kibana as:
 bigamat_2019

 echo "kibanaadmin:`openssl passwd -apr1`" | sudo tee -a /etc/nginx/htpasswd.users

 ### edited the enginx site-avalaible

 sudo nano /etc/nginx/sites-available/your_domain

 ### past:       server {
    listen 80;

    server_name your_domain;

    auth_basic "Restricted Access";
    auth_basic_user_file /etc/nginx/htpasswd.users;

    location / {
        proxy_pass http://localhost:5601;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
#### edited the dormain name sections

### created a link of the site-avalable in the site enable.

sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/your_domain

sudo nginx -t
sudo systemctl reload nginx

## in the web browser 
http://dormain nane/status


# Step3 install logstash

sudo apt install logstash

## created a configuration file called 02-beats-input.conf

sudo nano /etc/logstash/conf.d/02-beats-input.conf

### paste: input {
  beats {
    port => 5044
  }
}

## create another configuration file called 30-elasticsearch-output.conf

sudo nano /etc/logstash/conf.d/30-elasticsearch-output.conf

## paste:          output {
  if [@metadata][pipeline] {
	elasticsearch {
  	hosts => ["localhost:9200"]
  	manage_template => false
  	index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"
  	pipeline => "%{[@metadata][pipeline]}"
	}
  } else {
	elasticsearch {
  	hosts => ["localhost:9200"]
  	manage_template => false
  	index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"
	}
  }
}

## test if the logstach config is ok

sudo -u logstash /usr/share/logstash/bin/logstash --path.settings /etc/logstash -t

sudo systemctl start logstash

sudo systemctl enable logstash

# Step4 install and configure filebeat

sudo apt install filebeat

sudo nano /etc/filebeat/filebeat.yml

#### comment out the following:

...
#output.elasticsearch
 #array of host to connect to 
  #hostd: ["localhost:9200"]
...
#### and uncomment this:
output.lostash:
  # the logstash hosts
  hosts: ["localhost:5044"]

sudo filebeat modules enable system
sudo filebeat modules list
sudo filebeat setup --pipelines --modules system
sudo filebeat setup --index-management -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["localhost:9200"]'

# output
index seup finished 


sudo filebeat setup -E output.logstash.enabled=false -E output.elasticsearch.hosts=['localhost:9200'] -E setup.kibana.host=localhost:5601

after a few moment an ouput should be populated


sudo systemctl start filebeat

sudo systemctl enable filebeat


curl -XGET 'http://localhost:9200/filebeat-*/_search?pretty'