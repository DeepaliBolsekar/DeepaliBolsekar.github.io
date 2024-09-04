---
title: "Day-3"
date: 2024-09-03
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day3of30]
---

# Elasticsearch Setup

1. For this configuration, I utilized Vultr cloud service. To create the instance, I established a VPC in nearest region.
    
    ![vpc-create-1.png](/assets/ELK-setup/vpc-create-1.png){: width="500" height="300" }
    
2. Configure the network settings. I used IP range 172.31.0.0/24. Give a name to your VPC network and add the network by clicking on Add Network.
    
    ![vpc-network-config.png](/assets/ELK-setup/vpc-network-config.png){: width="500" height="300" }
    
3. Deploy the new server
    
    ![add-new-server.png](/assets/ELK-setup/add-new-server.png){: width="500" height="300" }
    
4. Choose type as dedicated CPU and same region as VPC.
    
    ![choose-type-mumbai.png](/assets/ELK-setup/choose-type-mumbai.png){: width="500" height="300" }
    
5. Choose Ubuntu 22.04 image for machine.
    
    ![choose-img-ubuntu.png](/assets/ELK-setup/choose-img-ubuntu.png){: width="500" height="300" }
    
6. Choose the plan suitable for elasticsearch 
    
    ![choose-plan-80gb.png](/assets/ELK-setup/choose-plan-80gb.png){: width="500" height="300" }
    
7. Choose the VPC we created for the elasticsearch server
    
    ![selected-vpc-for-instance.png](/assets/ELK-setup/selected-vpc-for-instance.png){: width="500" height="300" }
    
8. Don’t need the ssh key here for now, but give a name to your server
    
    ![deploy-instance.png](/assets/ELK-setup/deploy-instance.png){: width="500" height="300" }
    
9. Click the Deploy Now button and we successfully deployed our server.

**Install Elasticsearch:**

1. Update and upgrade packages: `sudo apt-get update && apt-get upgrade -y`
    
    ![update-machine.png](/assets/ELK-setup/update-machine.png){: width="500" height="300" }
    
    The Elasticsearch DEB package for x86_64 architecture can be downloaded directly from the official [Elasticsearch website](https://www.elastic.co/downloads/elasticsearch).
    
    ![elasticserch-download-page.png](/assets/ELK-setup/elasticserch-download-page.png){: width="500" height="300" }
    
2. Download Elasticsearch DEB package: `wget <download link>`
    
    ![download-elsaticsearch.png](/assets/ELK-setup/download-elsaticsearch.png){: width="500" height="300" }
    
3. Install Elasticsearch: `sudo dpkg -i <elasticsearch.deb>`
    
    After installing the Elasticsearch DEB package, important security configuration details will be displayed on the terminal. Make sure to record these settings, including the Elasticsearch password. This information is crucial for resetting passwords if needed.
    
    ![ls.png](/assets/ELK-setup/ls.png){: width="500" height="300" }
    
    ![unpack-elasticsearch.png](/assets/ELK-setup/unpack-elasticsearch.png){: width="500" height="300" }
    
    ![security-config.png](/assets/ELK-setup/security-config.png){: width="500" height="300" }
    

**Configure Elasticsearch:**

1. Navigate to the configuration file: `cd /etc/elasticsearch`
    
    ![cd-elasticsearch-dir.png](/assets/ELK-setup/cd-elasticsearch-dir.png){: width="500" height="300" }
    
2. Edit the configuration file: `nano elasticsearch.yml`
    
    By default, Elasticsearch is only accessible from the local host. For enhanced security and remote access, configure the network    host setting to your system's public IP address.
    
3. Uncomment and modify `network.host` and `http.port` settings to allow remote access.
    
    ![set-yml-file.png](/assets/ELK-setup/set-yml-file.png){: width="500" height="300" }
    

**Start Elasticsearch Service:**

To access Elasticsearch, we must activate and start the service after making the necessary changes.

1. Reload systemd daemon: `systemctl daemon-reload`
2. Enable Elasticsearch service at boot: `systemctl enable elasticsearch.service`
3. Start Elasticsearch service: `systemctl start elasticsearch.service`
    
![start-elasticsearch-service.png](/assets/ELK-setup/start-elasticsearch-service.png){: width="500" height="300" }
    

**Verify Service Status:**

- Check if Elasticsearch is running: `systemctl status elasticsearch.service`