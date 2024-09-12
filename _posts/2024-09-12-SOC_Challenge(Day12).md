---
title: "Day-12 Ubuntu-24.04 Server Installation"
date: 2024-09-12
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day12of30]
---


![Ubuntu-server](/assets/Ubuntu-24/server-title.png){: width="500" height="300" }

This is the time for creating our next server which is ubuntu server. According to logical diagram we will create a ubuntu server with ssh enabled as our target server and this is not inlcuded in our VPC just like windows server as per our last modification in logical diagram for our project infrastructure.

1. Let’s start with deploying the new server from vultr compute service.
    
    ![new-server.png](/assets/Ubuntu-24/new-server.png){: width="500" height="300" }
    
2. Choose the instance as shared CPU.
    
    ![shared-cpu-instance.png](/assets/Ubuntu-24/shared-cpu-instance.png){: width="500" height="300" }
    
3. Select the location same as all other servers you created.
    
    ![location-mumbai.png](/assets/Ubuntu-24/location-mumbai.png){: width="500" height="300" }
    
4. For image we are selecting Ubuntu 24.04 operating system.
    
    ![ubuntu-image.png](/assets/Ubuntu-24/ubuntu-image.png){: width="500" height="300" }
    
5. Now, we will select the Regular Cloud Compute plan with 1vCPU and 1GB memory.
    
    ![plan.png](/assets/Ubuntu-24/plan.png){: width="500" height="300" }
    
6. There is no need for any additional features so, let’s deselect all the selected features.
    
    ![no-additional-features.png](/assets/Ubuntu-24/no-additional-features.png){: width="500" height="300" }
    
7. Now, name your server and deploy the instance.
    
    ![servername-deploy-now.png](/assets/Ubuntu-24/servername-deploy-now.png){: width="500" height="300" }
    
    ![mydfir-linux-Cyberpenguine.png](/assets/Ubuntu-24/mydfir-linux-Cyberpenguine.png){: width="500" height="300" }
    
8. We will wait for few minutes for instance to run and then we will use SSH to access the server.
    
    ![ssh-into-instance.png](/assets/Ubuntu-24/ssh-into-instance.png){: width="500" height="300" }
    
9. First think to do after accessing the server is to update and upgrade the server using command:
    
    `#apt-get update && apt-get upgrade -y`
    
    ![update-instance.png](/assets/Ubuntu-24/update-instance.png){: width="500" height="300" }
    
10. As a SOC analyst we are interested in logs specifically authentication logs to find out who is trying to log into our server.
    
    ![var-log.png](/assets/Ubuntu-24/var-log.png){: width="500" height="300" }
    
11. Lets look at the authentication logs using `cat` command.
    
    `#cat auth.log`
    
    ![cat-authlog.png](/assets/Ubuntu-24/cat-authlog.png){: width="500" height="300" }
    
12. We can use `grep` command to look for specific keywords like failed, to display only the failed authentications from all the logs. `“ -i ”` is used for case-insensitive. It will search keyword regardless of the case of letters or word.
    
    `#cat auth.log | grep -i failed`
    
    ![failed-auth.png](/assets/Ubuntu-24/failed-auth.png){: width="500" height="300" }
    
13. As a root user we are more insterested in looking for the login attempts with root username. so, lets look for only root related failed attempts.
    
    `#cat auth.log | grep -i failed | grep -i root`
    
    ![root-auth-failed.png](/assets/Ubuntu-24/root-auth-failed.png){: width="500" height="300" }
    
14. We can also filter for specific column using `cut` command.
    
    `#cat auth.log | grep -i root | grep -i failed | cut -d ‘ ’ -f 9`
    
    `-d` is used to specify delimiter. here, the space is delimiter. it will seperate the columns as per the spaces.
    
    `-f` is used to specify the field and we want 9th column as per command above. So, it will seperate the columns by space and then display the 9th column.

    ![cut-1.png](/assets/Ubuntu-24/cut-1.png){: width="500" height="300" }
    
    ![cut-9.png](/assets/Ubuntu-24/cut-9.png){: width="500" height="300" }
    

These logs demonstrate a classic example of a brute force attack, a topic we covered in detail during Day 11's blog post.

While manually examining logs can be tedious, we'll explore tools like ELK in future posts to make this process more efficient.🤓

Explore further :

📑[Understanding Linux log](https://www.plesk.com/blog/featured/linux-logs-explained/)

🔖[Options available for cut](https://www.geeksforgeeks.org/cut-command-linux-examples/#options-available-in-cut-command) 

🔖[Options available for grep](https://www.geeksforgeeks.org/grep-command-in-unixlinux/#options-available-in-grep-command) 


