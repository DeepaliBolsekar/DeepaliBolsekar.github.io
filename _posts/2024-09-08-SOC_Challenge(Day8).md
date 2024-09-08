---
title: "Day-8 What is Sysmon?"
date: 2024-09-08
categories: [MYDFIR 30Day SOC_Challenge]
tags: [soc_challenge,soc,cybersecurity,day8of30]
---


![day-8](/assets/day-8.png)

The windows operating system logs the evnt by default but those are not in much detailed and it does not log the events like , process creation, network connection and file changes , which can be very useful for finding any malicious process created by malware after execution.  So, for advanced event logging we use sysmon.

- Sysmon, a tool used to monitor and log events on Windows, is commonly used by enterprises as part of their monitoring and logging solutions.
- As part of the Windows Sysinternals package, Sysmon is similar to Windows Event Logs with further detail and granular control.
- Sysmon gathers detailed and high-quality logs as well as event tarcing that assists in identifying anomalies in your environment.
- It is commonly used with a security information and event management (SIEM) system or other log parsing solutions that aggregate,filter, and visualize events.
- Sysmon includes 30 types of Event IDs, all of which can be used within the required configuration file to specify how the events should be handled and analyzed.

### Sysmon Overview

- From the Microsoft Docs, System Monitor (Sysmon) is a windows system services and device driver that, once installed on a system, remians resident across system reboots to monitor and log system activity to the windows event log.
- It provides detailed information about process creations, network connections, and changes to file creation time. By collecting the events it generates using Widnows Event Collection or SIEM agents and subsequently analyzing them, you can identify malicious or anomalous activity and understand how intruders and malware operate on your network.
- Sysmon gather detailed and high-quality logs as well as event tracing that assists in identifying anomalies in your environment.
- Events with sysmon are stored in Applications and Services Logs/Microsoft/Windows/……../Operational

### Sysmon Config Overview

- Sysmon requires a config file in order to tell the binary how to analyze the events that it is receiving.
- Can craete own sysmon config or download.
- Sysmon includes 30 different types of Event IDs .
- When creating or modifying configuration files you will notice that a majority of rules in sysmon-config will exclude events rather than include events. This will help filter out normal activity in your environment that will in turn decrease the number of events and alerts you will have to manually audit or search through in a SIEM.

### Event ID 1: Process Creation

- This event will look for any processes that have been created.
- Use to look for known suspicious processes with typos that would be considered an anomaly.
- The event will use the CommandLine and Image XML tags

### Event ID 3: Network Connection

- The network connection event will look for events that occur remotely.
- This will include files and source of suspicious binaries as well as opened ports.
- This event will use the Image and DestinationPort XML tags.

### Event ID 7: Image Loaded

- This event will look for DLLs loaded by processes, which is useful when hunting for DLL injection and DLL hijacking attacks.
- It is recommended to exercise caution when using this Event ID as it causes a high system load.
- This event will use the Image, Signed, ImageLoaded, and Signature XML tags.

### Event ID 8: CreateRemoteThread

- The CreateRemoteThread Event ID will monitor for processes injecting code into other processes.
- The CreateRemoteThread function is used for legitimate tasks and applications.
- However, it could be used by malware to hide malicious activity.
- This event will use the SourceImage, TargetImage, StartAddress, and StartFunction XML tags.

### Event ID 11: File Created

- This event id will log events when files are created or overwritten on the endpoint.
- This could be used to identify file names and signatures of files that are written to disk.
- This event uses TargetFilename XML tags.

### Event ID 12/ 13 / 14: Registry Event

- This event looks for changes or modifications to the registry.
- Malicious activity from the registry can include persistence and credential abuse.
- This event uses TargetObject XML tags

### Event ID 15: FileStreamHash

- This event will look for any files created in an alternate data stream.
- This is a common technique used by adversaries to hide malware.
- This event uses TargetFilename XML tags

### Event ID 22: DNS Event

- This event will log all DNS queries and events for analysis.
- The most common way to deal with these events is to exclude all trusted domains that you know will be very common “noise” in your environment.
- Once you get rid of the noise you can then look for DNS anomalies.
- This event uses QueryName XML tags.

The reference:  [https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)