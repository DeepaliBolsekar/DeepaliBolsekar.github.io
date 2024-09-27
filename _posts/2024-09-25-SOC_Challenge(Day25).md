---
title: "Day-25 osTicket and ELK integration"
date: 2024-09-25
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day25of30]
---


![day-25-cover](/assets/ticket&elk-integration/day-25-cover.png){: width="500" height="300" }

Today, we're wrapping up our environment setup for SOC investigations. We'll integrate osTicket with ELK. Let's start the instances, log into osTicket's Admin Panel, and get started.

![home-page.png](/assets/ticket&elk-integration/home-page.png){: width="500" height="300" }

Click on Manage option.

![manage.png](/assets/ticket&elk-integration/manage.png){: width="500" height="300" }

You'll see the API option there. Click on it, and then click on 'Add New API Key'.

![api.png](/assets/ticket&elk-integration/api.png){: width="500" height="300" }

To create an API, we'll need the private IP address of our ELK instance. You can find this by going to Settings > VPC 2.0 and copying the IP address.

![private-ip.png](/assets/ticket&elk-integration/private-ip.png){: width="500" height="300" }

Paste the IP address in the IP address field, check the box that says 'Can create ticket,' provide a description, and click 'Add key'.

![add-key.png](/assets/ticket&elk-integration/add-key.png){: width="500" height="300" }

In Manage tab you’ll see the API key generated.

![api-key.png](/assets/ticket&elk-integration/api-key.png){: width="500" height="300" }

Now, log in to Elastic with your credentials. From the hamburger menu icon, navigate to the Management section and select Stack Management.

![stack-manage.png](/assets/ticket&elk-integration/stack-manage.png){: width="500" height="300" }

To access all the options under 'Create Connector' in the 'Alerts and Insights' section, you'll need to start a 30-day free trial. Click on 'Manage License' to begin the trial.

![connectors.png](/assets/ticket&elk-integration/connectors.png){: width="500" height="300" }

![manage-license.png](/assets/ticket&elk-integration/manage-license.png){: width="500" height="300" }

Next, go to Connectors. To create a new connector, we'll use a webhook, which will send requests to a web service.

![webhook.png](/assets/ticket&elk-integration/webhook.png){: width="500" height="300" }

Let's get started! First, give your connector a name. Then, use a POST request with the correct URL for your OSticket instance. For now, we'll skip authentication. Next, add an HTTP header and include your API key.

![webhook-detail.png](/assets/ticket&elk-integration/webhook-detail.png){: width="500" height="300" }

Remember to save your configuration after making any changes. The changes won't take effect automatically unless you save them.

![save&test.png](/assets/ticket&elk-integration/save&test.png){: width="500" height="300" }

Next up, we'll need an XML payload for the body. Head over to the [osTicket GitHub page](https://github.com/osTicket/osTicket/blob/develop/setup/doc/api/tickets.md) to grab a pre-made XML body. Copy and paste it into the body field, and feel free to change the subject if you want. Keep everything else the same unless you have a reason to change it.

![xml-payload-github.png](/assets/ticket&elk-integration/xml-payload-github.png){: width="500" height="300" }

![test-fail.png](/assets/ticket&elk-integration/test-fail.png){: width="500" height="300" }

Our test failed with a bad request. Let's figure out what went wrong. First, let's try pinging our OSticket server using its private IP from the ELK server to see if it's accessible.

![ticket-private-ip.png](/assets/ticket&elk-integration/ticket-private-ip.png){: width="500" height="300" }

![host-unrecheable.png](/assets/ticket&elk-integration/host-unrecheable.png){: width="500" height="300" }

Looks like we're having some connectivity issues. We can't access it from the ELK server. Let's head over to the OSticket server to troubleshoot. You can find the OSticket server's IP address using the `ipconfig` command.

![no-private-ip.png](/assets/ticket&elk-integration/no-private-ip.png){: width="500" height="300" }

We see our public IP address, but the private IP is missing. Let's change that private IP from the Control Panel. Head to Network and Internet, then click on 'Change adapter settings.

![network.png](/assets/ticket&elk-integration/network.png){: width="500" height="300" }

![adapter-settings.png](/assets/ticket&elk-integration/adapter-settings.png){: width="500" height="300" }

Identify the network adapter you want to change, excluding any with public IP addresses. Modify the adapter's IP address to match the private IP of your OSticket server, and then save the changes.

![change-private-ip.png](/assets/ticket&elk-integration/change-private-ip.png){: width="500" height="300" }

Confirm by running the `ipconfig` command again.

![configrm-ip.png](/assets/ticket&elk-integration/configrm-ip.png){: width="500" height="300" }

As shown in the screenshot, the private IP address has been updated, and we can successfully ping it from the ELK server.

![can-ping-private-ip.png](/assets/ticket&elk-integration/can-ping-private-ip.png){: width="500" height="300" }

Let's modify the IP address in the POST URL of the connector and then rerun the test after saving the changes.

![change-ip-inconnector.png](/assets/ticket&elk-integration/change-ip-inconnector.png){: width="500" height="300" }

![test-success.png](/assets/ticket&elk-integration/test-success.png){: width="500" height="300" }

Success! The integration was a breeze. Head over to the OSticket Agent Panel to see the newly created ticket with the subject name we updated in the XML payload body. It's a small victory, but it's a step in the right direction!

![ticket-created.png](/assets/ticket&elk-integration/ticket-created.png){: width="500" height="300" }

We've successfully completed our environment setup. Stay tuned for more!