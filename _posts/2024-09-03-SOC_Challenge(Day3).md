---
title: "Day-3"
date: 2024-09-03
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day3of30]
---

# Elasticsearch Setup

For this configuration, I utilized an AWS EC2 instance. To create the instance, I established a VPC, subnet, route table, and internet gateway, connecting them appropriately. The instance was launched with specific settings for its name, AMI, firewall, and subnet. While AWS was my choice, you can adapt this process to any cloud service provider that suits your needs.

**Create a VPC:**

- Name: MYDFIR SOC Challenge
- IPv4 CIDR: 172.31.0.0/24
    
![VPC create](/assets/ELK-setup/vpc-create.png){: width="500" height="300" }
    

**Configure Firewall Group:**

Robust security settings are essential to ensure that only authorized individuals can access and utilize the service, mitigating potential risks.

- Allow inbound traffic from your IP address to Elasticsearch and Kibana ports.
- Enable remote access to the firewall group settings.

**Launch EC2 Instance:**

- Name: MYDFIR-ELK
- AMI: Ubuntu 22.04 x64
- Connect via SSH.
    
![ec2-name.png](/assets/ELK-setup/ec2-name.png){: width="500" height="300" }
    

![os-image-ubuntu.png](/assets/ELK-setup/os-image-ubuntu.png){: width="500" height="300" }

![ec2-selectvpc.png](/assets/ELK-setup/os-image-ubuntu.png){: width="500" height="300" }

![ec2-securitygroup(firewall-settings).png](/assets/ELK-setup/ec2-securitygroupfirewall-settings.png){: width="500" height="300" }

![running-instance.png](/assets/ELK-setup/running-instance.png){: width="500" height="300" }

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