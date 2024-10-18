
## Introduction

In this project, I deployed a mini honeynet in Azure, collecting log data from various sources. Microsoft Sentinel was used to create attack maps, trigger alerts, and generate incidents based on the collected data. Initially, I monitored the security metrics of the environment in its unsecured state for 24 hours. After applying security controls to harden the environment, I measured the same metrics over another 24-hour period. The results below compare the pre- and post-hardening security performance, focusing on key metrics such as:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/7EftgEP.jpeg)

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (1 windows, 1 linux)
- Azure Key Vault
- Azure Blob Storage Account
- Microsoft Sentinel

In the "BEFORE" phase, all resources were deployed with full exposure to the internet. Virtual Machines had completely open access through their Network Security Groups and built-in firewalls, and public endpoints for other resources were fully accessible online, with no implementation of Private Endpoints.

In the "AFTER" phase, Network Security Groups were tightened to block all traffic except from my admin workstation. Furthermore, built-in firewalls and Private Endpoints were applied to secure other resources and prevent unauthorized external access.

## Attack Maps Before Hardening / Security Controls
Without NSG controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/KzEJvwT.png)<br>
Linux Authentication failures
![Linux Syslog Auth Failures](https://i.imgur.com/zjceqai.png)<br>
Windows RDP Authentication failures
![Windows RDP/SMB Auth Failures](https://i.imgur.com/xFmCggT.png)<br>
MS SQL Authentication failures
![Microsoft SQL Brute Force Success](https://i.imgur.com/Y2ATwBR.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

Start Time 2024-10-14 22:04
Stop Time 2024-10-15 22:04

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 10849
| Syslog                   | 6196
| SecurityAlert            | 0
| SecurityIncident         | 369
| AzureNetworkAnalytics_CL | 4211

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our hardened environment after another 24 hours:

Start Time 2024-10-17 14:03
Stop Time	2024-10-18 14:03

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 1108
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was set up in Microsoft Azure, with various log sources integrated. These logs were processed using Microsoft Sentinel, which generated alerts and incidents based on the incoming data. Security metrics were initially gathered in the unsecured environment, and again after applying security measures. The results showed a significant drop in security events and incidents following the application of these controls, highlighting their effectiveness.

It's important to mention that if the network had been heavily accessed by regular users, there may have been an increase in security events and alerts during the 24-hour monitoring period after the security enhancements were implemented.
