---
title: "Day-30 Completed MYDFIR SOC Analyst 30 Day Challenge!"
date: 2024-09-30
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day30of30]
---

![30-day-cover](/assets/30-day-cover.png){: width="500" height="300" }

**Day 1: Creating Logical Diagram**

- Importance of logical diagrams for visualizing network infrastructure.
- Components: Windows Server (RDP), Fleet Server, Ubuntu Server (SSH), Elastic & Kibana, OS Ticket Server, C2 Server (Mythic), VULTR, VPC, Internet Gateway.

**Day 2: ELK Stack Introduction**

- Introduction to Elastic (search & analytics), Logstash (data collection), and Kibana (data visualization).
- Explains how these tools work together like a detective team.
- Briefly compares ELK to Splunk.

**Day 3: Elasticsearch Setup**

- Setting up Elasticsearch on a Vultr cloud instance.
- Covers installation, configuration, and service management.

**Day 4: Kibana Setup**

- Setting up Kibana on the same Vultr instance as Elasticsearch.
- Covers installation, configuration, access with enrollment token, and verification code.

**Day 5: Windows Server 2022 Installation**

- Creates a Windows server as a target machine for simulated attacks.
- Explains deployment on Vultr, access with RDP, and exposing RDP to the internet.

**Day 6: Elastic Agent and Fleet Server Introduction**

- Explains the role of Elastic Agent (universal data shipper) and Fleet Server (centralized management).
- Discusses benefits like centralized control, scalability, and improved visibility.
- Compares Elastic Agent to Beats modules.

**Day 7: Elastic Agent and Fleet Server Setup**

- Setting up Fleet Server on Vultr and integrating it with Elastic Agent.
- Covers server creation, policy generation, firewall configuration, and enrollment.
- Touches on troubleshooting common errors during enrollment.

**Day 8: What is Sysmon?**

- Explains Sysmon as a Windows tool for advanced event logging.
- Details the benefits of Sysmon compared to default Windows event logs.
- Covers Sysmon functionalities like process creation, network connections, and file changes.

**Day 9: Sysmon Setup**

- Setting up Sysmon on the target Windows server.
- Covers downloading, configuration, installation using PowerShell, and verification.

**Day 10: Elasticsearch Ingest Data Tutorial**

- Integrating Sysmon and Windows Defender logs with Elasticsearch.
- Explains adding integrations for each log source using the channel name and specific event IDs.
- Covers troubleshooting steps if data is not ingested properly.

 **Day 11: Brute Force Attacks**

- Hackers use trial-and-error to guess passwords, encryption keys, or other sensitive data.
- Methods include simple brute force attacks and dictionary attacks.
- Consequences include data theft, identity theft, financial loss, and reputation damage.

 **Day 12: Ubuntu Server Installation**

- You installed Ubuntu Server 24.04 and SSH.
- You used the `cat` and `grep` commands to examine authentication logs.
- These logs revealed a classic example of a brute force attack.

 **Day 13 & 14: Elastic Agent and Kibana**

- You installed the Elastic Agent on your Ubuntu server.
- You used Kibana to explore and analyze authentication logs.
- You created alerts and dashboards to monitor for suspicious activity.

 **Day 15: Remote Desktop Protocol**

- RDP allows remote access to computers but can be a security vulnerability.
- Attackers can use brute force attacks, credential stuffing, and other methods to exploit RDP.
- You learned methods to protect your RDP endpoints from attacks.

 **Day 16: Creating Rules and Alerts in Kibana**

- You created alerts for failed Windows authentication attempts.
- You created rules to detect unusual login patterns for SSH and RDP.

 **Day 17: Creating Dashboards and Visualizations**

- You built dashboards to visualize RDP successful and failed authentication attempts.
- You created visualizations for both SSH and RDP failed and successful authentication attempts.

**Day 18: Command and Control Introduction**

- Malicious links can lead to command-and-control (C2) servers.
- C2 servers allow attackers to maintain control over compromised systems.
- Popular C2 tools include Metasploit, Empire, Cobalt Strike, PowerSploit, and Mythic.

**Day 19: Creating Attack Diagram**

- Importance of understanding attacker strategy ("know your enemy")
- Planning an attack helps fortify defenses (ethical hacking)
- Introduction to MITRE ATT&CK framework and Cyber Kill Chain

**Day 20: Mythic Server Setup**

- Building a Mythic C2 server on Vultr cloud using Ubuntu
- Installation process using Docker commands
- Accessing the Mythic dashboard

**Day 21: Mythic Agent Setup**

- Setting up a brute force RDP attack on a Windows server
- Using Kali Linux with tools like Crowbar
- Creating a C2 agent on the Windows server using Mythic-CLI
- Downloading and executing the payload

**Day 22: Dashboard and Alerts for Mythic C2**

- Creating alerts for process creation, initialization, and Windows Defender disable
- Building a dashboard with visualizations for different event codes

**Day 23: Ticketing System**

- Introduction to ticketing systems (help desk, issue tracking)
- Benefits of using a ticketing system (organization, efficiency, communication)
- Key features of OSticket (open-source ticketing tool)

**Day 24: osTicket Setup**

- We deployed a new Windows Server instance for osTicket.
- We installed XAMPP (Apache, MySQL, PHP) on the server.
- We configured XAMPP and the database for osTicket.
- We downloaded and installed osTicket.
- We configured the osTicket installer and created an admin account.

**Day 25: osTicket and ELK Integration**

- We logged into the osTicket admin panel.
- We created a new API key in osTicket with the private IP address of the ELK instance.
- We logged into the Elastic GUI.
- We attempted to access the "Create Connector" option, but it requires a paid license.

**Day 26 & 27: Investigate SSH and RDP Brute-Force Attack**

- Configured OSticket to generate alerts for SSH/RDP brute-force attacks.
- Simulated attacks and investigated alerts in OSticket.

**Day 28: Investigate Mythic Agent**

- Analyzed Mythic Agent activity in Elastic.
- Identified suspicious activity and traced execution flow.
- Created a rule to detect Mythic Agent activity.

**Day 29: Elastic Defend**

- Set up Elastic Defend for EDR.
- Tested EDR functionality by attempting a malicious download.
- Observed successful prevention and alert generation.
- Analyzed alert details and configured a response action.
