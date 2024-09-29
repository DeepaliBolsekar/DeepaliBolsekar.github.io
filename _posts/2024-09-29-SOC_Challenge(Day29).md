---
title: "Day-29 Elastic Defend Setup"
date: 2024-09-29
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day29of30]
---

![cover](/assets/install-edr/day-29-cover.png){: width="500" height="300" }

Elastic has its own powerful endpoint protection solution called Elastic Defend. Today, we'll dive into installing Elastic Defend in our SOC environment to bolster our security posture.

## What is EDR?

Endpoint Detection and Response (EDR) is a security solution that monitors and responds to threats on endpoints, such as computers, mobile devices, and servers

### EDR can:

- **Detect threats:** EDR can identify and block threats across your network, including advanced and stealthy attacks.
- **Analyze threats:** EDR can provide information about the threat, including how it was initiated, where it's been, and what it's doing.
- **Respond to threats:** EDR can contain threats and prevent them from spreading, and can also roll back damage.
- **Protect networks:** EDR can protect your network by containing threats and preventing them from spreading.
- **Improve accuracy:** EDR uses machine learning and behavioral analysis to learn from historical data and improve its accuracy over time.
- **Detect zero-day attacks:** EDR can detect zero-day attacks and insider threats.
- **Detect emerging threats:** EDR can detect emerging threats like ransomware, novel malware, and advanced persistent threats (APT).
- **Provide visibility:** EDR provides security teams with real-time visibility into what's happening on endpoints.
- **Provide context:**  EDR provides threat hunters with the data and context they need to hunt for threats.

## Setup Elastic Defend

- Log in to your ELK using your credentials. Click on 'Integration' under the 'Management' section, which you can find in the hamburger menu icon.

![integration.png](/assets/install-edr/integration.png){: width="500" height="300" }

- Choose the Elastic Defend for integration. Then Add elastic defend.

![defend.png](/assets/install-edr/defend.png){: width="500" height="300" }

![add-elastic-defend.png](/assets/install-edr/add-elastic-defend.png){: width="500" height="300" }

- For configuration, provide a name for the integration to identify it and a brief description. Select the environment you want to protect. In this case, I am selecting the traditional endpoints for complete EDR.

![config-integration.png](/assets/install-edr/config-integration.png){: width="500" height="300" }

- Select the existing host. This is why we created fleet servers to have all the servers in one place. Now, select the Windows policy. Then, save and continue.

![agent-policy.png](/assets/install-edr/agent-policy.png){: width="500" height="300" }

- And deploy the changes.

![save-and-deploy.png](/assets/install-edr/save-and-deploy.png){: width="500" height="300" }

- Now, the redirected page will show the new integration policy for windows server.

![integration-created.png](/assets/install-edr/integration-created.png){: width="500" height="300" }

- To manage the endpoint we can go to Manage under Security and select the Endpoint option.

![manage.png](/assets/install-edr/manage.png){: width="500" height="300" }

![endpoint.png](/assets/install-edr/endpoint.png){: width="500" height="300" }

- From here, you can isolate the host. The "isolate host" option is available when you click on the three dots in front of your server's name.

![isolate-hosts.png](/assets/install-edr/isolate-hosts.png){: width="500" height="300" }

- Now, to test the settings we've made, we will try to download the payload file from the Mythic server on Windows.

![prevent-download.png](/assets/install-edr/prevent-download.png){: width="500" height="300" }

- And as you can see, we got the alert on the Windows server, and the file is not downloading as it is indicated as malware.

- Let's check the logs to see the details captured for this action.

![discover-1.png](/assets/install-edr/discover-1.png){: width="500" height="300" }

- In Discover, search for "malware" and sort the rows from newest to oldest to view the latest log.

- The log contains details about the actions you performed on Windows.

- It shows the instance name where the action occurred and the related component endpoint.

![discover-2.png](/assets/install-edr/discover-2.png){: width="500" height="300" }

- Let's move to the Alerts option under Security to see what it's showing.

![malware-prevention-alert.png](/assets/install-edr/malware-prevention-alert.png){: width="500" height="300" }

- We see a Malware Prevention Alert. Expanding the alert, you'll find details about the file name, file path, file hash, quarantined path, and more.

![alert-overview.png](/assets/install-edr/alert-overview.png){: width="500" height="300" }

- In the visualization, it will show where the action was performed. When I tried to download from PowerShell, it displayed the analyzer preview.

![visualization.png](/assets/install-edr/visualization.png){: width="500" height="300" }

![insights.png](/assets/install-edr/insights.png){: width="500" height="300" }

- We can create a response for our alert. It will perform the action we decided after such an incident, or if anyone tries to execute or download the malicious file on the endpoint.

- To do this, let's go to Rules under Security and click the option Edit rule settings.

![edit-rule-settings.png](/assets/install-edr/edit-rule-settings.png){: width="500" height="300" }

- From here choose the Response Action as Elastic Defend.

![responsive-action.png](/assets/install-edr/responsive-action.png){: width="500" height="300" }

- Then select the response action. Here I selected isolate host with brief description and save the changes.

![isolate.png](/assets/install-edr/isolate.png){: width="500" height="300" }

- Now, testing part.

- Go to the Windows server and start pinging Google DNS with the -t option for infinite pings.

- This indicates that our network is up and running.

![infinite-ping.png](/assets/install-edr/infinite-ping.png){: width="500" height="300" }

- Now, open powershell and again try downloading the payload from mythic.

![failed-download.png](/assets/install-edr/failed-download.png){: width="500" height="300" }

- A Malware Alert will be displayed, and the host will be isolated within a few seconds.

![host-isolated.png](/assets/install-edr/host-isolated.png){: width="500" height="300" }

- This testing confirms that our response is working effectively. This is our Security Operations Center (SOC) environment, which will help us collect and analyze logs, alerts, and endpoint detection and response.

Today, the SOC Analyst Challenge is complete. For the last day, I'll focus on troubleshooting and summarizing the 30-day journey to recap what I've accomplished in this challenge.