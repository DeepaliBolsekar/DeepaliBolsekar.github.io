---
title: "Day-20 Mythic C2 Setup"
date: 2024-09-20
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day20of30]
---


![day-20-cover](assets\Mythic-setup\day-20-cover.png){: width="500" height="300" }

Let's put our knowledge to the test and build our very own Mythic C2 server! First, we'll log into Vultr cloud using our credentials. 

- Then, we'll create a new server from the Compute options. 

![deploy-new-server.png](/assets/Mythic-setup/deploy-new-server.png){: width="500" height="300" }

- Opt for a cloud compute instance with shared CPU.

![shared-cpu.png](/assets/Mythic-setup/shared-cpu.png){: width="500" height="300" }

- Let's keep all the servers in the same location to avoid any geographical hiccups.

![location.png](/assets/Mythic-setup/location.png){: width="500" height="300" }

- Choose the image as Ubuntu 22.04 operating system for mythic instance.

![image.png](/assets/Mythic-setup/image.png){: width="500" height="300" }

- According to the docs, the Mythic server needs a minimum of 2 vCPUs and 4 GB of RAM to run smoothly. So, make sure your server is ready enough to handle the load!

![plan.png](/assets/Mythic-setup/plan.png){: width="500" height="300" }

- We're good to go! Let's deselect all the extra features we don't need.

![additional-feature.png](/assets/Mythic-setup/additional-feature.png){: width="500" height="300" }

- Now, let's label the server and get it ready for deployment.

![hostname&Deploy.png](/assets/Mythic-setup/hostname&Deploy.png){: width="500" height="300" }

- For our attack simulation, we'll be putting on our hacker hats and creating a Kali Linux virtual machine to act as the external attacker.

![download-kali-file-vm.png](/assets/Mythic-setup/download-kali-file-vm.png){: width="500" height="300" }

![i.png](/assets/Mythic-setup/i.png){: width="500" height="300" }

- There's a great tutorial out there that can walk you through setting up Kali Linux. Since we're focusing on Mythic in this blog, check out that tutorial for a step-by-step guide. https://youtu.be/wX75Z-4MEoM?t=580

- Now, let's SSH into the root user on your Mythic server using the command line. Once you're in, we'll install Docker using the following command

`#apt install docker-compose`

![install-docker-compose.png](/assets/Mythic-setup/install-docker-compose.png){: width="500" height="300" }

- Before we dive into Docker, we need to install a little helper called 'make.' Think of it as your personal assistant for building things. Here's how to add it to your toolkit:

`#apt install make`

![install-make.png](/assets/Mythic-setup/install-make.png){: width="500" height="300" }

- Now, we will clone the mythic feature from mythic official documentations.

`#git clone https://github.com/its-a-feature/Mythic`

![clone-feature.png](/assets/Mythic-setup/clone-feature.png){: width="500" height="300" }

- Let's take a peek inside the Mythic directory and see what files and folders are hiding there. Ready to explore?

![mythic-content.png](/assets/Mythic-setup/mythic-content.png){: width="500" height="300" }

- To fire up Mythic on Ubuntu, we'll need to get our Docker party started. Just run this magic command

`#./install_docker_ubuntu.sh`

![docker-ubuntu.png](/assets/Mythic-setup/docker-ubuntu.png){: width="500" height="300" }

- Run the following command to start the Docker container:

`#make`

![docker-error.png](/assets/Mythic-setup/docker-error.png){: width="500" height="300" }

- Looks like Docker is playing a bit of hide-and-seek. Let's troubleshoot by checking its status. Is it up and running?

`#systemctl status docker`

![not-active-docker.png](/assets/Mythic-setup/not-active-docker.png){: width="500" height="300" }

- Looks like Docker's taking a nap. Let's wake it up by starting the Docker service, then we can try running 'make' again.

`#systemctl start docker`

`#systemctl status docker`

`#make`

![docker-started.png](/assets/Mythic-setup/docker-started.png){: width="500" height="300" }


![make-docker.png](/assets/Mythic-setup/make-docker.png){: width="500" height="300" }

- It's time to fire up Mythic in our browser. But first, let's run the Mythic CLI.

`#./mythic-cli start`

![mythic-cli-start.png](/assets/Mythic-setup/mythic-cli-start.png){: width="500" height="300" }

- Wait a sec, are we missing something? Oh yeah, the firewall! We don't want just anyone poking around our Mythic server. Let's create a firewall group to keep it safe and sound.

![firewall.png](/assets/Mythic-setup/firewall.png){: width="500" height="300" }

- Add the firewall group:

![add-firewall-group.png](/assets/Mythic-setup/add-firewall-group.png){: width="500" height="300" }

- Keep this information under wraps! Share the IPs for our Ubuntu and Windows servers only with those who need access to Mythic. Let's keep this party private.

![add-rules.png](/assets/Mythic-setup/add-rules.png){: width="500" height="300" }

- Update the new firewall group created for mythic

![manage-mythic-firewall.png](/assets/Mythic-setup/manage-mythic-firewall.png){: width="500" height="300" }

![update-firewall.png](/assets/Mythic-setup/update-firewall.png){: width="500" height="300" }

- Let's paste that Mythic IP with port 7443 into your browser to access the dashboard. If you get a 'Bad Request' error, try switching to HTTPS. Just look for the 'Advanced' option and proceed.

![first-look-mythic.png](/assets/Mythic-setup/first-look-mythic.png){: width="500" height="300" }

![advanced-option.png](/assets/Mythic-setup/advanced-option.png){: width="500" height="300" }

- Here's a sneak peek of the Mythic dashboard, but don't worry about trying to log in just yet. We've got you covered.

![dashboard-mythic.png](/assets/Mythic-setup/dashboard-mythic.png){: width="500" height="300" }

- The password for your Mythic account is tucked away in the env file inside the Mythic folder.

![passwd.png](/assets/Mythic-setup/passwd.png){: width="500" height="300" }

- Since the  .env file is hidden, you'll need to use the command

`#ls -a`

to see it. Once you've located it, grab your password and log into your Mythic C2 server!

![mythic-homepage.png](/assets/Mythic-setup/mythic-homepage.png){: width="500" height="300" }

In our next blog, we'll dive deep into these fancy features you saw in the screenshot. Get ready to learn how can we use them! Stay tuned!