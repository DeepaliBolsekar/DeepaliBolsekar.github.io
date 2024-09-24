---
title: "Day-24 osTicket Setup"
date: 2024-09-24
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day24of30]
---



![day-24-cover](/assets/OsTicket/day-24-cover.png){: width="500" height="300" }

Yesterday, we talked about ticketing systems and OSticket. Today, let's dive into the setup. We'll start by creating a new server and deploying it. Get ready for some technical fun!

![new-server.png](/assets/OsTicket/new-server.png){: width="500" height="300" }

Select the 'shared CPU' option and choose the same location as the other servers we set up earlier.

![shared-cpu.png](/assets/OsTicket/shared-cpu.png){: width="500" height="300" }

![location.png](/assets/OsTicket/location.png){: width="500" height="300" }

Select the Windows Standard Server image as your operating system.

![win-img.png](/assets/OsTicket/win-img.png){: width="500" height="300" }

Opt for the regular plan with 1 vCPU and 2GB of memory.

![plan.png](/assets/OsTicket/plan.png){: width="500" height="300" }

From the additional features, we'll focus on the VPC option.

![vpc.png](/assets/OsTicket/vpc.png){: width="500" height="300" }

Let's give this instance a cool name and deploy it! Then, we'll add the MYDFIR-30-day-Challenge firewall to this OSticket Windows server. It's like adding a security guard to your digital castle.

![hostname.png](/assets/OsTicket/hostname.png){: width="500" height="300" }

Let's log into the OSticket server using RDP. Once inside, we'll need to install XAMPP, which is a crucial component for running OSticket.

![xampp-download.png](/assets/OsTicket/xampp-download.png){: width="500" height="300" }

Once you've downloaded the file, kick off the installation process and click 'OK' to dismiss any warning prompts that pop up.

![warning-ok.png](/assets/OsTicket/warning-ok.png){: width="500" height="300" }

Let it install.

![install-xampp.png](/assets/OsTicket/install-xampp.png){: width="500" height="300" }

While XAMPP is installing, let's set up a firewall rule for it. Since XAMPP uses ports 80 and 443, head over to Windows Defender Firewall and create a new inbound rule for port 80 and 443. Keep the default settings for now.

![create-new-rule.png](/assets/OsTicket/create-new-rule.png){: width="500" height="300" }

After a successful installation, the XAMPP control panel will pop up, and you'll see that the Apache server is running on ports 80 and 443. 

![start-xampp.png](/assets/OsTicket/start-xampp.png){: width="500" height="300" }

Next, click on the 'Admin' button right next to the 'Apache Start' button. A new webpage should pop up. From there, click on 'phpMyAdmin.

![phpmyadmin.png](/assets/OsTicket/phpmyadmin.png){: width="500" height="300" }

You'll be taken to the next page, where we'll make some changes to the user accounts for root and PMA. Let's update the hostname to match the IP address of the Windows OSticket server.

![user-acc.png](/assets/OsTicket/user-acc.png){: width="500" height="300" }

![root-acc-created.png](/assets/OsTicket/root-acc-created.png){: width="500" height="300" }

Be sure to update the PMA account credentials with the correct server IP address and password.

![pm-acc-created.png](/assets/OsTicket/pm-acc-created.png){: width="500" height="300" }

Once you've successfully installed XAMPP, the first thing you'll want to do is…

![acc-modified.png](/assets/OsTicket/acc-modified.png){: width="500" height="300" }

Let's tweak some settings in the XAMPP folder. Head over there and find the properties file. Change the domain name to your server's IP address, then save your changes. Easy peasy!

![properties.png](/assets/OsTicket/properties.png){: width="500" height="300" }

Next, find the `config.inc` file in the XAMPP > phpMyAdmin folder. Open it in a text editor. Change the password for the root user, the localhost IP address to the server IP, and the password for pma. Save the file.

![config.png](/assets/OsTicket/config.png){: width="500" height="300" }

Now, let’s create the database in phpMyAdmin for osTicket.

![db-create.png](/assets/OsTicket/db-create.png){: width="500" height="300" }

Let's get started! We're going to download the open-source osTicket software for our self-hosted ticketing system. 

![self-hosted.png](/assets/OsTicket/self-hosted.png){: width="500" height="300" }

![open-src-download.png](/assets/OsTicket/open-src-download.png){: width="500" height="300" }

To download osTicket, we'll follow these simple steps. First, choose the version you want. 

![release.png](/assets/OsTicket/release.png){: width="500" height="300" }

Next, choose your preferred language, but don't worry about plugins for now. Just skip that step and move on.

![lang.png](/assets/OsTicket/lang.png){: width="500" height="300" }

![plufins.png](/assets/OsTicket/plufins.png){: width="500" height="300" }

After this step, you'll see a prompt asking if you want to subscribe to the OSticket newsletter. Feel free to subscribe if you're interested, but I personally clicked 'No Thanks' for now.

Once you've downloaded the OSticket ZIP file, extract all the contents."

![extract-osticket.png](/assets/OsTicket/extract-osticket.png){: width="500" height="300" }

Copy the two folders you see above, scripts and uploads, and paste them into a new folder named 'osticket' inside the 'htdocs' folder. The 'htdocs' folder is usually located within the 'xampp' folder.

![copy-to-htdocs.png](/assets/OsTicket/copy-to-htdocs.png){: width="500" height="300" }

Now, you can access the OSticket installer using your server's public IP address. Just go to <server-ip>/osticket/upload and you'll see a page like the one in the screenshot.

![osticket-installer.png](/assets/OsTicket/osticket-installer.png){: width="500" height="300" }

Click the 'Continue' button at the bottom and follow the on-screen instructions. Rename the file 'ost-sampleconfig' to 'ost-config'. You'll find this file in the following directory: xampp > htdocs > osTicket > upload > include.

![ost-config.png](/assets/OsTicket/ost-config.png){: width="500" height="300" }

Next up, we'll dive into the form and create your account. Remember to keep your username and password handy for future logins to the staff control panel.

![instal-fields-1.png](/assets/OsTicket/instal-fields-1.png){: width="500" height="300" }

Then click on install now.

![install-now.png](/assets/OsTicket/install-now.png){: width="500" height="300" }

You might run into the same issue I did: you probably forgot to create the database for OSticket or didn't give the root user permission. I made that mistake too, but I realized it later. Let's fix that by granting the database the necessary privileges.

![select-db.png](/assets/OsTicket/select-db.png){: width="500" height="300" }

![privileges.png](/assets/OsTicket/privileges.png){: width="500" height="300" }

One possible reason for the error is that you might have accidentally typed in 'localhost' instead of the server's public IP address when filling out the installation form. I made that mistake too! To fix it, simply replace 'localhost' with the correct server IP address.

![again-install-now.png](/assets/OsTicket/again-install-now.png){: width="500" height="300" }

Great! It's working as it should. Let's give it a few seconds to do its thing.

![doing-stuff-page.png](/assets/OsTicket/doing-stuff-page.png){: width="500" height="300" }

The next page will prompt us to reset the ost-config file. Following the instructions, let's execute the command task.

![file-perm.png](/assets/OsTicket/file-perm.png){: width="500" height="300" }

![success.png](/assets/OsTicket/success.png){: width="500" height="300" }

Bookmark those links to the staff control panel for easy access later!

![copy-staff-contrl-panel.png](/assets/OsTicket/copy-staff-contrl-panel.png){: width="500" height="300" }

Now, let's use the link for the staff control panel. Log in using the same credentials you created during the installer setup.

![staff-login.png](/assets/OsTicket/staff-login.png){: width="500" height="300" }

Once you log in successfully, you'll be greeted by the admin panel. This is where the magic happens! From here, you can customize and tweak your admin panel to your liking.

![admin-panel.png](/assets/OsTicket/admin-panel.png){: width="500" height="300" }

This is where the magic happens! You'll see tickets pouring in from clients, and you'll be the one handling them. You can even create new agents and manage other settings.

We've successfully set up our ticketing system. In our next blog, we'll dive into the nitty-gritty of analyzing logs. Stay tuned for more SOC adventures!