---
title: "Day-5"
date: 2024-09-05
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day5of30]
---

# Windows Server 2022 Installation

**Today, we'll focus on creating our Windows server as a target machine.** This server will play a crucial role in our simulated attack scenarios, following the logic diagram we established on Day 1.

**Let's get started:**

1. **Launch a New Vultr Server:**
    - Log in to your Vultr account and go to compute option.
    - Click on "Deploy New Server".
        
        ![new-server.png](/assets/Win-server/new-server.png){: width="500" height="300" }
        
    - Choose "Cloud Compute - Shared CPU" as the server type.
        
        ![select-type.png](/assets/Win-server/select-type.png){: width="500" height="300" }
        
    - Select the same location as your VPC and ELK instance for optimal network connectivity.
        
        ![choose-location.png](/assets/Win-server/choose-location.png){: width="500" height="300" }
        
    - For the image, select "Windows Standard 2022 Server".
        
        ![win-image.png](/assets/Win-server/win-image.png){: width="500" height="300" }
        
    - Choose a suitable plan, such as the "Regular Cloud Compute" with 1 vCPU, 2GB RAM, and 55GB SSD storage.
        
        ![select-plan.png](/assets/Win-server/select-plan.png){: width="500" height="300" }
        
    
    - Do not choose any Additional Features for Win-server. We will not add it to VPC as per our modification in logical diagram below.
        
        ![no-additional-features.png](/assets/Win-server/no-additional-features.png){: width="500" height="300" }
        
    
2. **Isolate the Windows Server:**
- Let's adjust our logic diagram from Day 1. We'll place the Windows server and Ubuntu server outside the VPC. This means they'll be accessible from the internet but won't have access to the private network used by other servers within the VPC. This isolation will help prevent any potential compromise of the Windows server from affecting the rest of our setup.
    
    ![Modified-Logic-Diagram.drawio.png](/assets/Win-server/Modified-Logic-Diagram.drawio.png){: width="500" height="300" }
    
1. **Deploy and Access the Server:**
    - Give your server a meaningful name and deploy it.
        
        ![server-hostname.png](/assets/Win-server/server-hostname.png){: width="500" height="300" }
        
        ![deployed-win-server.png](/assets/Win-server/deployed-win-server.png){: width="500" height="300" }
        
    
    - Once deployed, open the server and click "Show Extra Keys"(with symbol ‘A’).
        
        ![clt-alt-del-key.png](/assets/Win-server/clt-alt-del-key.png){: width="500" height="300" }
        
    - Then click on option Send Ctrl+Alt+Del (Three dots) to send a keyboard interrupt and log in using the provided credentials.
        
        ![put-win-pass.png](/assets/Win-server/put-win-pass.png){: width="500" height="300" }
        
        ![running-windows.png](/assets/Win-server/running-windows.png){: width="500" height="300" }
        
2. **Expose RDP:**
    - Ensure that Remote Desktop Protocol (RDP) is exposed to the internet. This will allow you to access the server remotely.
    - To verify, copy the server's public IP address and try connecting to it using RDP on your system.
        
        ![rdp-exposed.png](/assets/Win-server/rdp-exposed.png){: width="500" height="300" }
        

**That's it for today!** We've successfully deployed the Windows server. In the next blog post, we'll focus on configuring it for its role in our simulated attacks.