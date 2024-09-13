---
title: "Day-13 Installing Elastic Agent on Ubuntu Server"
date: 2024-09-13
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day13of30]
---





On day 12 we sucessfully installed the Ubuntu server 24.04 and now that we've successfully set up our Ubuntu 24.04 server, let's proceed with installing the Fleet agent. Let’s start with loging to our vultr account and starting the machines.

- Go to elasticsearch and login to your account. Click on hamburger icon and under Management select Fleet.

![fleet-under-management.png](/assets/Ubuntu-24/Fleet-integration/fleet-under-management.png){: width="500" height="300" }

- On the fleet page, you'll find the "Agent Policies" option. Click on it and create a new agent policy for your Ubuntu server.

![agent-policies.png](/assets/Ubuntu-24/Fleet-integration/agent-policies.png){: width="500" height="300" }

- Choose a policy name that aligns with the MYDFIR challenge, such as "MYDFIR-Linux-Policy." However, feel free to select a name that better reflects your specific requirements or preferences.

![create-agent-policy.png](/assets/Ubuntu-24/Fleet-integration/create-agent-policy.png){: width="500" height="300" }

- To create a policy for your Ubuntu server, click on "Create agent policy." The newly created policy will appear in the "Agent Policies" tab.

![agent-policy-created.png](/assets/Ubuntu-24/Fleet-integration/agent-policy-created.png){: width="500" height="300" }

- Locate the agent policy you created and click on the integration's name. In my case, it's called 'system-3,' but yours may be different.

![click-system-3.png](/assets/Ubuntu-24/Fleet-integration/click-system-3.png){: width="500" height="300" }

- You'll be viewing the logs collected for your Ubuntu server. For Ubuntu, the primary log file is `/var/log/auth.log`. Redhat/CentOS systems use `/var/log/secure`. For now, we'll focus on these files for ubuntu server. So, let’s keep the file paths as it is.

![log-paths.png](/assets/Ubuntu-24/Fleet-integration/log-paths.png){: width="500" height="300" }

- Now, lets create an agent. Go to Agent tab and click on Add agent button. 

![add-agent.png](/assets/Ubuntu-24/Fleet-integration/add-agent.png){: width="500" height="300" }

- To add the agent, specify the name of the policy you created for the Ubuntu server and enroll it in Fleet, as recommended.

![select-linux-policy.png](/assets/Ubuntu-24/Fleet-integration/select-linux-policy.png){: width="500" height="300" }

![enroll-in-fleet.png](/assets/Ubuntu-24/Fleet-integration/enroll-in-fleet.png){: width="500" height="300" }

- To utilize the fleet, we'll need to install it on our Ubuntu server.

    - Locate the appropriate command for Linux.
    - Paste the copied command into your Ubuntu server's terminal and press Enter to begin the installation process.

![copy-command.png](/assets/Ubuntu-24/Fleet-integration/copy-command.png){: width="500" height="300" }

![install-fleet-agent.png](/assets/Ubuntu-24/Fleet-integration/install-fleet-agent.png){: width="500" height="300" }

- To continue the installation, type "y" and enter.

![yes.png](/assets/Ubuntu-24/Fleet-integration/yes.png){: width="500" height="300" }

- If you encounter an error like the one I did while installing the Fleet agent, stating "Certificate signed by unknown authority," you might recall that we've addressed this issue previously during the Windows Fleet installation.

- This error typically arises due to the use of a self-signed certificate for Fleet agent installation.

![failed-install.png](/assets/Ubuntu-24/Fleet-integration/failed-install.png){: width="500" height="300" }

- To resolve the error, we'll append the `--insecure` flag to the end of the command and run it again. This should successfully install the Fleet agent on our Ubuntu server.

![success-install.png](/assets/Ubuntu-24/Fleet-integration/success-install.png){: width="500" height="300" }

- Once the Fleet agent is successfully installed on the Ubuntu server, the Elasticsearch screen will display the message "Agent Enrollment and Incoming Data Confirmed.”

![confirmed.png](/assets/Ubuntu-24/Fleet-integration/confirmed.png){: width="500" height="300" }

- Let's explore our logs using the Discover tab. To verify the connection, locate your agent name in the left-side navigation pane. If you don't see it, try refreshing Elasticsearch in your browser. Once you've selected the agent name, you'll be able to view all associated logs.

![discover-1.png](/assets/Ubuntu-24/Fleet-integration/discover-1.png){: width="500" height="300" }

- On Day 12, while reviewing the`/var/log/auth.log`file, we identified a suspicious IP address associated with failed root authentication attempts. Let's investigate further by searching for related logs on Elasticsearch.

![failed-log-ip.png](/assets/Ubuntu-24/Fleet-integration/failed-log-ip.png){: width="500" height="300" }

![discover-2.png](/assets/Ubuntu-24/Fleet-integration/discover-2.png){: width="500" height="300" }

You can view the search results related to your query.

In Day 12's blog, we explored the challenges of manually analyzing logs directly on the terminal. However, Elasticsearch has significantly simplified this process, allowing us to efficiently search, filter, and sort our results based on specific criteria.