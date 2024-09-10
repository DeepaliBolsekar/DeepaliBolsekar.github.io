---
title: "Day-10 Elasticsearch Ingest Data"
date: 2024-09-10
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day10of30]
---




To view data in Elasticsearch, we will need to ingest the data using integration. By ingesting the data, we will be able to search through all the logs obtained from Windows Defender and Sysmon on Elasticsearch. Let's begin today's task of the MYDFIR SOC Analyst Challenge.

- Log in to your Elasticsearch instance. On the homepage, you'll find a button labeled "Add Integrations". Click on this button to access a list of available integrations.

![Add-integration-btn.png](/assets/integration/Add-integration-btn.png){: width="500" height="300" }

- We are interested in Sysmon and Windows event logs, so we will search for them.

- We will search Windows event logs to collect Windows logs.

![windows-event-logs-opt.png](/assets/integration/windows-event-logs-opt.png){: width="500" height="300" }

- Click on the option that says "Custom Windows Event Logs." On the right-hand side, you'll see the button to add the integration. Click on that.

![add-cutom-win-logs.png](/assets/integration/add-cutom-win-logs.png){: width="500" height="300" }

- To integrate mydfir-sysmon-winlog1, provide the requested details. For the channel name, go to Event Viewer on your Windows server instance and search for sysmon. Right-click on the “Operational” under sysmon folder, select Properties, and in the General tab, locate the Full Name option. The value in the Full Name field is your channel name.

![sysmon-channelname.png](/assets/integration/sysmon-channelname.png){: width="500" height="300" }

![channel-name-sysmon.png](/assets/integration/channel-name-sysmon.png){: width="500" height="300" }

- Then leave everything as default.

- For "Where to add this integration?", we'll add the existing host MYDFIR-Windows-Policy, then click on save and continue.

![existing-host-win.png](/assets/integration/existing-host-win.png){: width="500" height="300" }

- Now, the sysmon integration is added to our policy.

![save-deploy-changes.png](/assets/integration/save-deploy-changes.png){: width="500" height="300" }

- Let's do the same for our Windows Defender logs. Click on "Add Integration" on the right side. Then fill in the required information. For the channel name, in Event Viewer, go to Windows Defender folder, right-click on "Operational," select "Properties," and copy the "Full Name" from the "General" tab.

![winDefender-channel-name.png](/assets/integration/winDefender-channel-name.png){: width="500" height="300" }

![channel-name-win-defender.png](/assets/integration/channel-name-win-defender.png){: width="500" height="300" }

- Next, click on Advanced Options. We want to add the specific Event IDs for this challenge, so we will include 1116, 1117, and 5001 separated by commas in the Event ID field. For the location of integration, we will choose MYDFIR-Windows-Policy

![advanced-opt-event-id-add.png](/assets/integration/advanced-opt-event-id-add.png){: width="500" height="300" }

![exisiting-host-win.png](/assets/integration/exisiting-host-win.png){: width="500" height="300" }

- Click on "Save and Continue," then "Save and deploy changes."

- If you want to exclude the event IDs, simply place a minus sign in front of each ID.

- We have added integration for both Sysmon and Windows Defender as shown in below screenshot.

![custom-win-event-logs.png](/assets/integration/custom-win-event-logs.png){: width="500" height="300" }

- To test this, go to Discover from the hamburger menu and search for sysmon. If you are unable to find sysmon or there are no search results, then let's troubleshoot:

![no-logs.png](/assets/integration/no-logs.png){: width="500" height="300" }

1. Go to the "Integration" option under "Management" by clicking on the hamburger icon. Search for the "event_id" field. Copy this field and paste it into the search bar on the "Discover" page. Can you see "sysmon" under "data_stream_dataset"? If not, then…move to another method for troubleshooting
    
    ![data_stream_Dataset.png](/assets/integration/data_stream_Dataset.png){: width="500" height="300" }
    
2. Go to the "Fleet" section under "Management." Locate the instance named "mydfir-win-<username>" and select it. Check if any logs have been collected. If not, navigate to "Services" on the Windows Server instance and restart the "Elastic Agent" service by right-clicking on it. Are logs still not appearing?
    
    ![elastic-restart.png](/assets/integration/elastic-restart.png){: width="500" height="300" }
    
3. Check the CPU status in the agent details of mydfir-win-<username>. If it shows 'N/A,' this indicates a connectivity issue between the agent and Elasticsearch. To resolve this, go to the firewall rules we created for this challenge and add a rule to allow incoming connections to your server using the TCP protocol on port 9200, with 'Anywhere' as the source. Wait a few minutes, then refresh the winlogs in Fleet > Agents > mydfir-win-<username>. You should now see values for CPU and Memory in the Agent Details, indicating that the connection is working. Finally, go to the Logs tab and verify that logs are visible.
    
    ![cpu.png](/assets/integration/cpu.png){: width="500" height="300" }
    
    ![firewall-rule.png](/assets/integration/firewall-rule.png){: width="500" height="300" }
    

- Next, go to Discover, enter the event ID, and look for search results with the event provider 'Sysmon'.

![discover-logs.png](/assets/integration/discover-logs.png){: width="500" height="300" }

![see-event-provider-sysmon.png](/assets/integration/see-event-provider-sysmon.png){: width="500" height="300" }

![log-win-defender.png](/assets/integration/log-win-defender.png){: width="500" height="300" }

We successfully ingested Windows event logs into Elasticsearch.

If you're swimming in a sea of confusion, don't hesitate to [reach out to me.](https://www.linkedin.com/in/deepali-bolsekar-77676b191/).