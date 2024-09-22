---
title: "Day-22 Mythic Dashboard and Alert in Kibana"
date: 2024-09-22
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day22of30]
---




In this blog, we will continue our ritual and create the alerts and dashboard for mythic c2.

The alerts will contain the information regarding the process creation, initialization and winodws defender disable alerts.

- To create the alerts we’ll need to create a suitable query for our first alert.

- Create alert for svchost payload file and event code to find the related logs easily and the fields required to us.

![1.png](/assets/Mythic-Dashboard/1.png){: width="500" height="300" }

- After updating the query we can expand the log and see the Hash for payload file. Let’s store that hash for further investigations and alert creation.

![2.png](/assets/Mythic-Dashboard/2.png){: width="500" height="300" }

- We can look into virustotal for any flags against the payload.

![searching-hash.png](/assets/Mythic-Dashboard/searching-hash.png){: width="500" height="300" }

- As you can see this hash has no flags as malicious because it is freshly created payload.

- If search a little more you’ll see the original filename of payload file in log fields. Let’s tae this field for alert.

![original-filename.png](/assets/Mythic-Dashboard/original-filename.png){: width="500" height="300" }

- This will be our final query for alert which includes event code as 1 which indicates the process creation, file hash, original filename with or condition. The or condition is used because we want either the original file as apollo or the matching hash for malicious payload. we removed the payload name because the name can be anything for payload.

![remove-filename.png](/assets/Mythic-Dashboard/remove-filename.png){: width="500" height="300" }

- Now save the search.

![mythic-apollo-process-create-search-save.png](/assets/Mythic-Dashboard/mythic-apollo-process-create-search-save.png){: width="500" height="300" }

- Now, next task is to create the rules,

![rules-option.png](/assets/Mythic-Dashboard/rules-option.png){: width="500" height="300" }

- In rules choose the Detection SIEM rules option.

![detection-rules-siem.png](/assets/Mythic-Dashboard/detection-rules-siem.png){: width="500" height="300" }

- Click on Create New Rule button,

![create-new-rule.png](/assets/Mythic-Dashboard/create-new-rule.png){: width="500" height="300" }

- Choose Custom Query button and paste the query we created for search.

![custom-query.png](/assets/Mythic-Dashboard/custom-query.png){: width="500" height="300" }

- Keep the index pattern default.

![query.png](/assets/Mythic-Dashboard/query.png){: width="500" height="300" }

- You can choose the required field as I did. These fields are basic for log analysis and very useful as well. But if you think you need different than these, you can continue with other fields as well. Ultimate goal is your understanding for logs.

![required-fields.png](/assets/Mythic-Dashboard/required-fields.png){: width="500" height="300" }

- Give appropriate rule name and keep the default severity as Critical.

![agent-rule.png](/assets/Mythic-Dashboard/agent-rule.png){: width="500" height="300" }

- Set the schedule t run every 5 minutes and additional look back for 5 minutes.

![schedule-rule.png](/assets/Mythic-Dashboard/schedule-rule.png){: width="500" height="300" }

- we’ll keep the rule action default settings and Create & enable the rule.

![default-rule-action.png](/assets/Mythic-Dashboard/default-rule-action.png){: width="500" height="300" }

![rule-created.png](/assets/Mythic-Dashboard/rule-created.png){: width="500" height="300" }

- We have a dashboard created previously for authentication activity but I would like to create a new fresh dashboard. So, let’s create new Dashboard.

![create-dashboard.png](/assets/Mythic-Dashboard/create-dashboard.png){: width="500" height="300" }

- Now, create visualization by using the queries for different event codes for different processes.

![visualization.png](/assets/Mythic-Dashboard/visualization.png){: width="500" height="300" }

- First query with event code 1 as process creation with required fields.

    - Event ID 1: event.code:1 and event.provider:Microsoft-Windows-Sysmon and (powershell or cmd or rundll32)

*host.hostname*

*winlog.event_data.CommandLine*

*winlog.event_data.Image*

*winlog.event_data.ParentCommandLine*

*winlog.event_data.ParentImage*

*winlog.event_data.ProcessGuid*

*winlog.event_data.User*

*winlog.event_data.CurrentDirectory*

![eventcode-1.png](/assets/Mythic-Dashboard/eventcode-1.png){: width="500" height="300" }

- Here modify the values as 999 and change the names of fields for ease.

- For next query with event code 3 with shows the process nitialization.

    - Event Id 3: event.code:3 and event.provider:Microsoft-Windows-Sysmon and winlog.event_data.Initiated:true and not winlog.event_data.Image:*MsMpEng.exe

*winlog.event_data.Image*

*winlog.event_data.SourceIp*

*winlog.event_data.DestinationIP*

*winlog.event_data.DestinationPort*

![eventcode-3.png](/assets/Mythic-Dashboard/eventcode-3.png){: width="500" height="300" }

- Do the same changes as above.

- And for 3rd query we will use event code 5001. For windows defender disable alert.

    - Event Id 5001: event.code:5001 and event.provider:Microsoft-Windows-Windows Defender

*host.hostname*

*winlog.event_data.Product name*

*event.code*

![eventcode-5001.png](/assets/Mythic-Dashboard/eventcode-5001.png){: width="500" height="300" }

- Everytime you create visualization do not forget to click on save and return button.

- Now, this how the dashboard will look like with three new visualizations.

![dashboard.png](/assets/Mythic-Dashboard/dashboard.png){: width="500" height="300" }

- Don’t forget to save the dashboard.

![save-dashboard.png](/assets/Mythic-Dashboard/save-dashboard.png){: width="500" height="300" }

- And done.

![dashboard-saved.png](/assets/Mythic-Dashboard/dashboard-saved.png){: width="500" height="300" }

Today we practiced creating alerts and dashboard for mythic. If you have any suggestion or doubts please reach out to me on linkedin. Stay tuned for next informative blog.