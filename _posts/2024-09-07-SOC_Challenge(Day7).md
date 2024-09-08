---
title: "Day-7 Fleet Server and Elastic Agent setup"
date: 2024-09-07
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day7of30]
---


![day-7](assets/day-7.png)

We will continue with setting up fleet server and integrating it with elastic agent.
Login to vultr account we created with login credentials.

1. **Creating Fleet Server**
    
    - In vultr, go to compute option and click **Deploy** button and deploy new server for fleet server creation.
    
    ![new-server.png](/assets/FleetServer&ElasticAgentSetup/new-server.png){: width="500" height="300" }
    
    - For the fleet server we will be using **Dedicated CPU** instance.
    
    ![dedicated-cpu-type.png](/assets/FleetServer&ElasticAgentSetup/dedicated-cpu-type.png){: width="500" height="300" }
    
    - Keep the location for fleet server as same as our VPC.
    
    ![location-mum.png](/assets/FleetServer&ElasticAgentSetup/location-mum.png){: width="500" height="300" }
    
    - For image we will be using the **Ubuntu 22.04** image.
    
    ![image-ubuntu.png](/assets/FleetServer&ElasticAgentSetup/image-ubuntu.png){: width="500" height="300" }
    
    - Let’s select a suitable plan as per requirements with 1 vCPU, 4GB memory and 30GB storage
    
    ![plan.png](/assets/FleetServer&ElasticAgentSetup/plan.png){: width="500" height="300" }
    
    - For additional features we don not require backup and IPv6 features. But As per our logic diagram the fleet server is inside the VPC so, we will be selecting the VPC 2.0. 
    
    ![aaditional-features.png](/assets/FleetServer&ElasticAgentSetup/aaditional-features.png){: width="500" height="300" }
    
    - Next. choose the appropriate VPC for the fleet server. 
    
    ![selected-vpc.png](/assets/FleetServer&ElasticAgentSetup/selected-vpc.png){: width="500" height="300" }
    
    - To make it easy for us to identify our server, let’s name it as MYDFIR-Fleet-Server and click Delpoy now and our server will be ready.
    
    ![server-hostname.png](/assets/FleetServer&ElasticAgentSetup/server-hostname.png){: width="500" height="300" }
    
2. **Add fleet server**
    
    - Now, access the kibana interface through the web browser using your IP and port as 5601.
    
    - Click on hamburger icon, scroll down to Management and select fleet.
    
    - Click on “Add Fleet Server” button.
    
    ![add-fleet-server.png](/assets/FleetServer&ElasticAgentSetup/add-fleet-server.png){: width="500" height="300" }
    
    - For this challenge we will go with “Quick Start” as it will be good for personal project but for production environment we will be using Advanced option.
    
    ![quicke-start.png](/assets/FleetServer&ElasticAgentSetup/quicke-start.png){: width="500" height="300" }
    
    - Basic steps for generating fleet server policy are required, so let’s start with name and then URL.
    
    - Here URL will be the IP address of fleet server we created.
    
    ![generate-fleet-server-policy.png](/assets/FleetServer&ElasticAgentSetup/generate-fleet-server-policy.png){: width="500" height="300" }
    
    - Now, proceed by clicking the “Generate Fleet Server Policy” button.
    
    - After few minutes the policy will be created and we can proceed with the further installation of fleet server creation.
    
    - But before that we need to complete some prerequisites like:
    
    - Adding the Fleet Server IP to MYDFIR firewall group as a rule by allowing port range 1-65535 with protocol TCP.
    
    ![firewall-rule.png](/assets/FleetServer&ElasticAgentSetup/firewall-rule.png){: width="500" height="300" }
    
    - Then update the firewall group and wait for 120 seconds for the rule to apply.
    
    ![update-firewall-group.png](/assets/FleetServer&ElasticAgentSetup/update-firewall-group.png){: width="500" height="300" }
    

    - And in ELK server allow port 9200 in firewall using `ufw allow 9200`

    - This port is used for communication between Elasticsearch clients and the Elasticsearch server, allowing clients to send search queries, indexing data, and retrieving data.

    ![allow-9200.png](/assets/FleetServer&ElasticAgentSetup/allow-9200.png){: width="500" height="300" }

    - Continuing with our installation now, copy the policy created and  paste it in fleet server’s terminal and enter.

    ![fleet-server-installation.png](/assets/FleetServer&ElasticAgentSetup/fleet-server-installation.png){: width="500" height="300" }

    - After successful execution of commands in fleet server terminal, connection will be established.

    ![fleet-server-connected.png](/assets/FleetServer&ElasticAgentSetup/fleet-server-connected.png){: width="500" height="300" }

    - Now, click on “Continue enrolling Elastic Agent”.

3. **Adding the elastic agent to host:**
    
    - Now, let’s add the agent to our host. Here, the host is Windows server which we created earlier.
    
    ![add-agent.png](/assets/FleetServer&ElasticAgentSetup/add-agent.png){: width="500" height="300" }
    
    - Give the name to the policy for windows server and click “Create Policy”.
    
    ![windows-policy.png](/assets/FleetServer&ElasticAgentSetup/windows-policy.png){: width="500" height="300" }
    
    - To install Agent on windows host use the given command on windows powershell.
    
    ![host-installation.png](/assets/FleetServer&ElasticAgentSetup/host-installation.png){: width="500" height="300" }
    
    - Paste it in our windows server powershell with administrator privilege.
    
    ![win-error.png](/assets/FleetServer&ElasticAgentSetup/win-error.png){: width="500" height="300" }
    
    - As you can see, it’s showing an error, to troubleshoot this error. look at what this error is saying (fail to execute request to fleet-server).
    
    - You can look for the error on internet and can find the solution as allowing the necessary ports. The fleet server have few default ports we will need to allow. We will allow 8220 for Elastic Agent —> Fleet Server communication.
    
    ![default-port-assignment.png](/assets/FleetServer&ElasticAgentSetup/default-port-assignment.png){: width="500" height="300" }
    
    - Using command line : `ufw allow 8220` we can add the port to fleet server firewall. 
    
    ![allow-8200.png](/assets/FleetServer&ElasticAgentSetup/allow-8200.png){: width="500" height="300" }
    
    - Then run the windows commands again.
    
    - Again encountering the error so, now we will go to elasticsearch interface, click on hamburger icon, select the Fleet under Management option. In settings we will change the port to 8220. Save and apply the changes.
    
    ![port-change-to-8220.png](/assets/FleetServer&ElasticAgentSetup/port-change-to-8220.png){: width="500" height="300" }
    
    - Now, modify the command with 8220 port instead of 443 and run the commands on windows server again.
    
    ![port-change-on-win.png](/assets/FleetServer&ElasticAgentSetup/port-change-on-win.png){: width="500" height="300" }
    
    - Now, again it displays an error with certificate because we are using self-signed certificate for Quick Start setup option.
    
    ![x509-cert-error.png](/assets/FleetServer&ElasticAgentSetup/x509-cert-error.png){: width="500" height="300" }
    
    - To deal with this error we will add `--insecure` at the end of the command and run it again. Now, it will successfully install the agent on host.
    
    ![agent-insalled-on-win.png](/assets/FleetServer&ElasticAgentSetup/agent-insalled-on-win.png){: width="500" height="300" }
    
    - Go to fleet server agent on kibana interface on browser and now, we have our windows host.
    
    ![done.png](/assets/FleetServer&ElasticAgentSetup/done.png){: width="500" height="300" }
    
    - We can go to “Discover” option to see some logs if there are any.
    
    ![logs-visible.png](/assets/FleetServer&ElasticAgentSetup/logs-visible.png){: width="500" height="300" }
    
    - So, here are some logs for us to search using fields.
    
    - We successfully completed the setup of fleet server and integration of elastic agent.