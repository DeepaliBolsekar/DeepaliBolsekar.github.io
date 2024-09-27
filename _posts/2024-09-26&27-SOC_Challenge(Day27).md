---
title: "Day-26 and 27 Brute Force Attack Investigation"
date: 2024-09-27
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day26of30,day27of30]
---

![day26&27-cover](/assets/log-analysis/day-26&27.png){: width="500" height="300" }

Let's start by creating some rules to streamline our alert management in OSticket. Head over to the 'Alerts' section under 'Security' (you'll find it by clicking the hamburger icon). From there, click 'Manage rules.

![manage-rules.png](/assets/log-analysis/manage-rules.png){: width="500" height="300" }

Select the SSH-Brute-Force rule.

![ssh-brute-force.png](/assets/log-analysis/ssh-brute-force.png){: width="500" height="300" }

Now Edit rule settings

![edit-rules-settings.png](/assets/log-analysis/edit-rules-settings.png){: width="500" height="300" }

In the rule settings, select 'Webhook' from the 'Actions' menu.

![actions-webhood.png](/assets/log-analysis/actions-webhood.png){: width="500" height="300" }

Keep everything the same, and paste the XML body from the OSticket XML payload GitHub page, just like we did on Day 25. However, remove the attachments and IP tag from the XML code and replace the name, subject, and message with your own.

![create-body.png](/assets/log-analysis/create-body.png){: width="500" height="300" }

These variables can be used to retrieve information from OSticket. We've successfully created the rule using them.

![rule-created.png](/assets/log-analysis/rule-created.png){: width="500" height="300" }

Let’s do the same for RDP-Brute-Force rule.

![rdp-brute-force.png](/assets/log-analysis/rdp-brute-force.png){: width="500" height="300" }

![edit-rule-rdp.png](/assets/log-analysis/edit-rule-rdp.png){: width="500" height="300" }

![webhook-rdp.png](/assets/log-analysis/webhook-rdp.png){: width="500" height="300" }

![rdp-webhook-body.png](/assets/log-analysis/rdp-webhook-body.png){: width="500" height="300" }

![rdp-created.png](/assets/log-analysis/rule-created.png){: width="500" height="300" }

Imagine this: You're chilling in the osTicket staff panel, sipping your virtual coffee, when BAM! An alert pops up. 

![rpd-osticket.png](/assets/log-analysis/rpd-osticket.png){: width="500" height="300" }

From there, you can follow our standard process for investigating log alerts, assign the alert to yourself, and document your findings. 

![process.png](/assets/log-analysis/process.png){: width="500" height="300" }

Once you've addressed the alert, close the ticket. You'll find closed tickets in the 'Closed' tab, saving you time and effort.

![rdp-closed-ticket.png](/assets/log-analysis/rdp-closed-ticket.png){: width="500" height="300" }

That's a wrap for today's blog! Stay tuned for more exciting content in the future. If you have any suggestions or feedback, don't hesitate to reach out.