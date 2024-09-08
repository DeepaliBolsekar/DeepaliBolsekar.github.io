---
title: "Day-4 Kibana Setup"
date: 2024-09-04
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day4of30]
---

![day-4](assets/day-4.png)

Alright, let's move on to setting up Kibana on our Day 3 adventure! Here's how we'll access the Kibana interface using your server's public IP:

**1. Download and Install Kibana:**

- Open your server instance on Vultr.
- Head over to the Kibana download page and copy the download link for the DEB package (similar to what we did for Elasticsearch).
- Download Kibana using the following command, replacing `<kibana….deb>` with the [actual link:](https://artifacts.elastic.co/downloads/kibana/kibana-8.15.0-amd64.deb)
    
    `#wget <kibana….deb>`
    
    ![kibana-download.png](/assets/kibana/kibana-download.png){: width="500" height="300" }
    

- Unpack the downloaded file:
    
    `#dpkg -i <kibana….deb>`
    
    ![unpack kibana.png](/assets/kibana/unpack kibana.png){: width="500" height="300" }
    

**2. Kibana Configuration:**

- Now, let's edit the Kibana configuration file. Go to the directory containing the file and use nano to edit it:
    
    `#cd /etc/kibana`

    `#nano kibana.yml`
    
    ![kibana-yml-edit.png](/assets/kibana/kibana-yml-edit.png){: width="500" height="300" }
    
- Look for the `server.host` setting and edit it to match your server's public IP address.
- While you're at it, uncomment both the `server.host` and `server.port` settings.

**3. Start and Verify Kibana:**

- We need to reload the system daemon, enable the Kibana service at boot, and then start the service itself. Run these commands one by one:
    
    `#systemctl daemon-reload`

    `#systemctl enable kibana.service`

    `#systemctl start kibana.service`

    `#systemctl status kibana.service`
    
    ![kibana-start-service.png](/assets/kibana/kibana-start-service.png){: width="500" height="300" }
    

- The last command will show the status of the Kibana service. Verify that it's running.

**4. Generate Enrollment Token:**

- To access Kibana, we'll need a special token. Let's change directories first:
    
    `#cd /usr/share/elasticsearch/bin`
    
- Now, generate the token using the following command:
    
    `#./elasticsearch -create-enrollment-token --scope kibana`
    
    ![enrollment-token.png](/assets/kibana/enrollment-token.png){: width="500" height="300" }
    
- Copy the generated token.

**5. Access Kibana Interface:**

- Open a web browser and navigate to your server's public IP address, followed by the Kibana port number (usually 5601).
    
    ![error-connection-timeout.png](/assets/kibana/error-connection-timeout.png){: width="500" height="300" }
    

**Troubleshooting:**

- If you encounter a "site unreachable" or "timeout" error, you might need to adjust your firewall settings. Add a rule to allow access on port 5601 and restart the firewall service.
    
    ![firewall-for-port-5601.png](/assets/kibana/firewall-for-port-5601.png){: width="500" height="300" }
    
- And if still it’s not working then you can use commands like `#ufw allow 5601` for firewall management.
    
    ![ufw-allow-port.png](/assets/kibana/ufw-allow-port.png){: width="500" height="300" }
    
- Once you've addressed the firewall issue, refresh the page in your browser. Now, you should be able to see the Kibana interface.
    
    ![kibana-interface.png](/assets/kibana/kibana-interface.png){: width="500" height="300" }
    

**6. Login to Kibana:**

- On the interface, you'll be prompted to enter the enrollment token. Paste the token you copied earlier and click "Configure Elastic".
    
    ![paste-enrollment-token.png](/assets/kibana/paste-enrollment-token.png){: width="500" height="300" }
    

**7. Verification Code:**

- To get the verification code, navigate back to your server instance and run:
    
    `#cd /usr/share/kibana/bin`

    `#ls`  This will list available commands
    
    `#./kibana-verification-code`
    
    ![verify-token-prompt.png](/assets/kibana/verify-token-prompt.png){: width="500" height="300" }
    
    ![got-verfication-code.png](/assets/kibana/got-verfication-code.png){: width="500" height="300" }
    

- Copy the verification code displayed.
    
    ![code-put.png](/assets/kibana/code-put.png){: width="500" height="300" }
    

**8. Enter Credentials:**

- Now, you should see a login prompt. Remember that security configuration screen you got earlier? Use the username and password listed there (usually username: "elastic" and password found in the configuration). Enter these credentials and log in.
    
    ![login.png](/assets/kibana/login.png){: width="500" height="300" }
    
    ![elasticsearch-interface.png](/assets/kibana/elasticsearch-interface.png){: width="500" height="300" }
    

**9. Encryption Keys:**

- The last step involves adding encryption keys. Click on the hamburger menu (three horizontal lines) in Kibana, then navigate to Security > Alert. You'll see an alert prompting you to add encryption keys.
    
    ![alerts.png](/assets/kibana/alerts.png){: width="500" height="300" }
    
    ![API-integration.png](/assets/kibana/API-integration.png){: width="500" height="300" }
    

- Back on your server instance, navigate to:
    
    `#cd /usr/share/kibana/bin`

    `#./kibana-encryption-keys generate`
    
    ![kibana-encryption-keys.png](/assets/kibana/kibana-encryption-keys.png){: width="500" height="300" }
    

- Copy the keys displayed in the "Settings" section and paste them into a notepad.
- Use the following command (replacing `<name_of_the_key_without_colon>` with the actual name) to add each key:
    
    `#./kibana-keystore add  <name_of_the_key_without_colon>`
    
    ![API-integration-keyadded.png](/assets/kibana/API-integration-keyadded.png){: width="500" height="300" }
    

- You'll be prompted to enter a value; provide it, and repeat this two more times to add all three keys.

**10. Restart and Enjoy!**

- Finally, restart the Kibana service:
    
    `#systemctl restart kibana.service`
    
- Go back to your browser, refresh the page, and enter your credentials. 
- Now, you should be able to enjoy using the Kibana interface!
    
    ![api-integration-warning-gone.png](/assets/kibana/api-integration-warning-gone.png){: width="500" height="300" }


