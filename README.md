# SOC / Honeynet Architecture in Azure + Security Hardening
![Cloud Honeynet / SOC](https://imgur.com/t98Qqpx.jpg)

## Introduction

In this project detailed below, I constructed a mini honeynet in Azure and ingested logs from various resources into Log Analytics workspace. I then analyzed the SOC / honeynet environment with live traffic. This was accomplished with the use of Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. Security metrics were measured in an insecure environment for a total of 24 hours. I subsequently implemented security controls to harden the environment, which metrics were measured for another 24. The metrics measured were:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://imgur.com/9wx4mAq.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://imgur.com/SedUWr1.jpg)

Components of the Azure mini honeynet's architecture:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

"BEFORE" metrics insights: - all resources were deployed in full exposure to the internet. Both Network Security Groups and built-in firewalls wide open on the vitural machines. All other resources are deployed with public endpoints, visible to the internet with no use of Private Endpoints.

"AFTER" metrics insights: Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation. All other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://imgur.com/PDrEwD6.jpg)<br>
![Linux Syslog Auth Failures](https://imgur.com/FVqXOjg.jpg)<br>
![Windows RDP/SMB Auth Failures](https://imgur.com/Qn0IUAL.jpg)<br>

## Metrics Before Hardening / Security Controls

Insecure environment metrics without security controls | measured for 24 hours period:
Start Time 2024-05-12 12:42:54
Stop Time 2024-05-13 12:42:54

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 6362
| Syslog                   | 9865
| SecurityAlert            | 0
| SecurityIncident         | 163
| AzureNetworkAnalytics_CL | 2368

## Attack Maps Before Hardening / Security Controls

```Map queries returned 'no results' after 24 hour period due to successful implementation of hardening techniques ```

## Metrics After Hardening / Security Controls

Secure environment metrics after applying security controls | measured for 24 hours period:
Start Time 2024-05-14 5:48:12
Stop Time 2024-05-15 5:48:12

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 2577
| Syslog                   | 7
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## End Results
Impact of security controls

| Metric                   | %
| ------------------------ | -----
| SecurityEvent            | -59.49%
| Syslog                   | -99.93%
| SecurityAlert            | 0
| SecurityIncident         | -100%
| AzureNetworkAnalytics_CL | -100%

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
