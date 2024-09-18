---
title: "Day-18 Command and Control Introduction"
date: 2024-09-18
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day18of30]
---



![Day-18](/assets/day-18.png){: width="500" height="300" }

Have you ever clicked on a seemingly harmless link only to find your device acting strangely? If so, you might have fallen victim to a malicious link. This blog post will delve into the mechanics of these attacks, explore the concept of command-and-control (C2) servers, and discuss the tools used by attackers.

### **What happens when you click on a malicious link?**

When you click on a malicious link, you're essentially inviting a digital intruder into your device.

Here's a breakdown of what typically happens from an attacker's perspective:

1. **Landing Page:** The malicious link usually leads to a specially crafted webpage. This webpage might appear harmless, but it contains malicious code designed to exploit vulnerabilities in your device or browser.
2. **Exploit Delivery:** The webpage delivers the malicious code to your device. This could be in the form of a malicious script, a downloadable file, or even a simple redirect to another harmful website.
3. **Vulnerability Exploitation:** If your device or browser has known vulnerabilities, the malicious code can exploit them to gain unauthorized access. This might involve executing malicious code on your device or bypassing security measures.
4. **Payload Delivery:** Once the attacker has gained a foothold, they can deliver their payload. This could be anything from malware that steals your personal information to ransomware that locks your files until you pay a ransom.
5. **Data Collection:** The malicious software on your device can start collecting information about you and your system. This might include your browsing history, login credentials, credit card details, or even your location.
6. **Exfiltration:** The collected data is then sent back to the attacker's servers, where it can be analyzed and exploited for further attacks or sold on the dark web.

![day-18-comic](/assets/day-18-comic-scene.png){: width="500" height="300" }

### What is C2? 🤔

Let’s understand the C2 in a very simple way through a scenario.

Imagine your computer is a castle. You're the king or queen, and your commands are the royal decrees that control the castle's operations.

Now, imagine a malicious hacker as a sneaky spy. They want to take over your castle and control its resources. To do this, they need a way to communicate with their minions inside the castle and give them orders.

This secret communication channel is called a command-and-control (C&C) server. It's like a hidden spy headquarters where the hacker can send instructions to their malware agents lurking on your computer.

For example**,** if the hacker wants to steal your bank account information, they might send a command to their malware agent saying, "Go to the banking website and steal the user's login credentials." The malware agent, obediently following the hacker's orders, would try to log into your bank account using the information it finds on your computer.

So, in a nutshell, a C&C server is the hacker's secret base of operations, allowing them to control their malicious minions and wreak havoc on your digital kingdom.

To know technical aspect of how command and control works you can refer the MITRE ATT&CK. It can also explains the techniques.

### Why is it important to establish for attackers?🧐

Establishing a command-and-control (C&C) server is crucial for attackers for several reasons:

1. **Persistent Control:** A C&C server allows attackers to maintain long-term control over compromised systems. This means they can continue to access and exploit these systems even after initial infection, making it difficult for defenders to detect and eradicate the threat.
2. **Centralized Command:** A C&C server acts as a central hub for coordinating and managing multiple compromised systems. Attackers can use it to send commands, receive updates, and exfiltrate stolen data from various targets.
3. **Scalability:** C&C servers can be designed to handle large-scale botnets, enabling attackers to launch more powerful and sophisticated attacks. They can easily add or remove compromised systems from the network, making it difficult for defenders to disrupt the operation.
4. **Stealth:** C&C servers can be configured to be stealthy, making them difficult to detect and track. Attackers can use techniques like encryption, tunneling, and dynamic IP addresses to hide their communications and avoid detection.
5. **Persistence:** C&C servers can be set up to automatically reconnect if the connection is lost, ensuring that the attacker maintains control over compromised systems even in the face of network disruptions or security measures.
    
    In essence, a C&C server is the backbone of a successful attack campaign**.** It provides attackers with the tools and infrastructure they need to maintain persistent control, coordinate attacks, and maximize their impact.
    

### What are some of the tools / frameworks?⚙️

C2 (Command and Control) tools and frameworks are essential for attackers to maintain persistent control over compromised systems. Here are some popular options:

**Open-Source Tools**

- **Metasploit:** A well-known penetration testing framework that can be used for C2 operations. It offers a wide range of exploits, payloads, and auxiliary modules.
- **Empire:** A PowerShell-based post-exploitation framework that provides advanced C2 capabilities, including lateral movement, privilege escalation, and persistence.
- **Cobalt Strike:** A commercial penetration testing tool that can be used for C2, offering features like beacon payloads, pivoting, and tunneling.
- **PowerSploit:** A PowerShell exploitation framework that can be used to execute various attacks and establish C2.
- **Mythic:** Mythic uses a web-based front end (React) and Docker containers for the back-end. A GoLang server handles the bulk of the web requests via GraphQL APIs and WebSockets.

**Commercial Tools**

- **DarkCloud:** A commercial C2 platform that offers advanced features like persistence, tunneling, and encryption.
- **Remote Access Trojan (RAT):** RATs like TeamViewer, AnyDesk, and UltraVNC can be used for C2 purposes, although they are primarily designed for legitimate remote access.

**Custom Frameworks**

- **Custom-built C2 frameworks:** Attackers may develop their own C2 frameworks to avoid detection and maintain control over their botnets. These frameworks can be tailored to specific needs and can be more difficult to detect and disrupt.

### What is mythic and how does it work?🕵️

Mythic is a highly customizable and extensible C2 framework written in Python. It offers a wide range of features, making it a popular choice among both red teamers and blue teamers.

**Key Features of Mythic:**

- **Customization:** Mythic allows for extensive customization, enabling attackers to tailor the framework to their specific needs and preferences.
- **Extensibility:** The framework is highly extensible, allowing users to create custom payloads, agents, and modules.
- **Stealth:** Mythic is designed to be stealthy, with features like encryption, tunneling, and obfuscation to avoid detection.
- **Cross-Platform Compatibility:** Mythic supports various operating systems, including Windows, Linux, and macOS.
- **Advanced Features:** Mythic offers advanced features such as post-exploitation techniques, lateral movement, privilege escalation, and persistence.

**Mythic's C2 Architecture:**

- **Server:** The Mythic server is the central hub that manages communication with the agents. It provides a web-based interface for controlling the framework and monitoring agent activity.
- **Agents:** Agents are the malicious payloads that are deployed on compromised systems. They communicate with the server and execute commands.
- **Stager:** The stager is a small, initial payload that is used to deploy the full agent on the target system.
    
    Mythic is a powerful tool that can be used for both offensive and defensive security purposes. It is a valuable asset for red teams conducting penetration testing and blue teams defending against advanced threats.
    

🔖References and further explore:

[C2 : MITRE ATT&CK](https://attack.mitre.org/tactics/TA0011/)

[C2 : Palo alto networks](https://www.paloaltonetworks.com/cyberpedia/command-and-control-explained#:~:text=The%20C2%20server%20sends%20instructions,%2C%20email%2C%20and%20custom%20protocols)

[Mythics documentation](https://docs.mythic-c2.net/)