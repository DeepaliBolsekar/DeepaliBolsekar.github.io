---
title: "Day-9 Setting up Sysmon"
date: 2024-09-09
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day9of30]
---

# Sysmon Setup

In our previous blog, we introduced Sysmon. Now, let's set it up on our Windows server. Start your previously created Vultr Windows server instance. Use RDP for remote access.

![RDP.png](/assets/sysmon-setup/RDP.png){: width="500" height="300" }

- Search for "Sysmon Sysinternals" online. Download the latest Windows version. 

![sysmon-download.png](/assets/sysmon-setup/sysmon-download.png){: width="500" height="300" }

- Extract the downloaded files.

![extract-files.png](/assets/sysmon-setup/extract-files.png){: width="500" height="300" }

- For Sysmon configuration, use the Olaf GitHub repository. Search for "Olafhartong Sysmon config" and download the `sysmonconfig.xml` file. 

![sysmon-config.png](/assets/sysmon-setup/sysmon-config.png){: width="500" height="300" }

- Place it in the extracted Sysmon folder.

![config-save-in-sysmon.png](/assets/sysmon-setup/config-save-in-sysmon.png){: width="500" height="300" }

- Check if Sysmon is already installed in Event Viewer > Applications and  Service logs > Microsoft > Windows and Services. 

![no-sysmon-in-services.png](/assets/sysmon-setup/no-sysmon-in-services.png){: width="500" height="300" }

![no-sysmon-eventviewer.png](/assets/sysmon-setup/no-sysmon-eventviewer.png){: width="500" height="300" }

- If not, proceed with the following:

- Open PowerShell as an administrator. Change the directory to the folder where we extracted the sysmon. Then,

![cd-powershell.png](/assets/sysmon-setup/cd-powershell.png){: width="500" height="300" }

- Type `.\sysmon64.exe` in PowerShell to see available options.

![sysmon-options.png](/assets/sysmon-setup/sysmon-options.png){: width="500" height="300" }

- Install Sysmon using:

`.\sysmon64.exe -i sysmonconfig.xml`

![agreement.png](/assets/sysmon-setup/agreement.png){: width="500" height="300" }

- Agree the Licence Agreement and the installation will be done.

![installed-sysmon.png](/assets/sysmon-setup/installed-sysmon.png){: width="500" height="300" }

- Refresh Services and Event Viewer > Applications and  Service logs > Microsoft > Windows to verify Sysmon's status.

![eventviewer-sysmon.png](/assets/sysmon-setup/eventviewer-sysmon.png){: width="500" height="300" }

![service-sysmon.png](/assets/sysmon-setup/service-sysmon.png){: width="500" height="300" }