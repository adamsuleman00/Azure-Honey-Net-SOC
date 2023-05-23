# Azure Honeynet Project: Simulating Real-World Cyber Attacks
[![Cloud Honeynet / SOC](https://github.com/asuleman-cyber/Azure-Honey-Net-SOC/blob/main/Cloud%20Honeynet%20%2B%20SOC.png)

## Introduction
In this project, I have developed a honeynet in Azure to simulate real-world cyber attacks. By integrating log sources from various resources into a Log Analytics workspace, I leverage Microsoft Sentinel to generate attack maps, trigger alerts, and create incidents. I measured security metrics in an insecure environment for 24 hours, implemented security controls to strengthen the environment, and measured metrics for another 24 hours. The results are presented below, showcasing the metrics obtained.

## Objective
The purpose of this initiative was to enhance my knowledge of attacker tactics and techniques, as well as demonstrate my understanding in incident response and environment hardening.

## Security Metrics Used for Queries in the Log Analytics Workspace
- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://github.com/asuleman-cyber/Azure-Honey-Net-SOC/blob/main/Insecure%20Architecture.png)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://github.com/asuleman-cyber/Azure-Honey-Net-SOC/blob/main/Secure%20Architecture.png)

## Environments and Architecture Technologies Used
- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault for Secure Secrets Management
- Azure Storage Account for Data Storage
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- Microsoft Defender for Cloud to Protect Cloud Resources
- Windows Remote Desktop for Remote Access
- Command Line Interface (CLI) for System Management
- PowerShell for Automation and Configuration Management
- NIST SP 800-53 Security Controls (Rev 4)
- NIST SP 800-61 Incident Handling Guidance (Ref 2)

For the "BEFORE" metrics, all resources were initially deployed with open exposure to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls configured with unrestricted access, and all other resources were deployed with public endpoints visible to the internet, without utilizing Private Endpoints.

For the "AFTER" metrics, I implemented significant security enhancements. Firstly, I strengthened the Network Security Groups by blocking ALL traffic except for access from my admin workstation. Moreover, I ensured that all resources were protected by their respective built-in firewalls and implemented a v-net with its own network security group for added security measures. Additionally, I closed the exposed ports (RDP/SSH) on the VMs. To further enhance security, I enabled the use of Private Endpoints. Furthermore, firewall rules were configured to allow access only from my workstation PC for the purpose of gathering log traffic data in the environment.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://imgur.com/kyzhWTy.png)<br>
![Linux Syslog Auth Failures](https://imgur.com/gPhkKLT.png)<br>
![Windows RDP/SMB Auth Failures](https://imgur.com/Jhfkoh6.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-05-12 21:39:41
Stop Time 2023-06-12 22:25:35

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 34411
| Syslog                   | 933
| SecurityAlert            | 6
| SecurityIncident         | 150
| AzureNetworkAnalytics_CL | 647

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-05-15 18:23:10
Stop Time	 2023-06-15 20:34:21

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Approach to Handling High-Priority Incidents with NIST Guidelines and Security Controls
To handle high-priority incidents effectively, I followed the guidelines provided by NIST 800-61 (Revision 2) and implemented the security controls outlined in NIST SP 800-53 (Revision 4). Here's how I approached the process:

1. First, I made the necessary preparations by setting up a log analytics workspace, configuring Azure Sentinel, and establishing alerts to detect incidents. To ensure a robust and secure environment, I implemented security controls from NIST SP 800-53.
2. When incidents occurred, I assigned them accordingly and evaluated their severity. I carefully inspected logs, conducted investigations to determine if they were false or true positives, and assessed the scope of their impact. Throughout this process, I relied on the incident response procedures outlined in NIST 800-61 (Revision 2).
3. To streamline my incident response efforts, I utilized an incident response playbook based on NIST 800-61 (Revision 2). This playbook allowed me to comprehensively document all incident details. Additionally, I incorporated the relevant security controls from NIST SP 800-53 (Revision 4) to guide my incident response activities.
4. Once the incidents were resolved, I diligently documented my findings, including the steps taken and the analysis performed. I then closed out each incident, indicating its resolution and any necessary follow-up actions. It was crucial for me to ensure compliance with the applicable security controls from NIST SP 800-53 (Revision 4) during the closure process.

## Balancing Costs and Data Integrity
![Lab Cost](https://imgur.com/K0hP21y.png )
Considerably reducing costs was possible by turning off the VMs nightly. However, this approach would have interrupted traffic ingestion into the logs, impacting data analysis and incident response capabilities.

## Conclusion
In this project, I built a honeynet in Microsoft Azure, integrating log sources into a log analytics workspace. Additionally, I deployed Azure Sentinel to generate alerts and incidents using the log data. I measured metrics 24 hours after creating the insecure resources and another 24 hours after implementing security controls. The metric data tables clearly demonstrate a significant decrease in incidents, highlighting the effectiveness of the implemented security controls.

Please note that this project was conducted in a controlled environment, and the results may vary depending on the specific situation and context in which they are applied.
