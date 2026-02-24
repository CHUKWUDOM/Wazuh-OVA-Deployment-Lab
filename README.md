# Wazuh-OVA-Deployment-Lab
## VirtualBox All-in-One Setup

### 📌 Project Overview

This project documents the deployment of the official all-in-one OVA image of [Wazuh](https://wazuh.com/) using [VirtualBox](https://www.virtualbox.org/).

The objective of this lab is to:

* Deploy a preconfigured Wazuh SIEM appliance
* Configure NAT networking with port forwarding
* Validate core services (Manager, Indexer, Dashboard)
* Compare OVA deployment with manual installation
* Prepare for a full Home SOC multi-VM architecture

This project represents Phase 2 of a structured SOC lab progression.
<br>
_____________________________________________________________________________
## Architecture Overview

The all-in-one OVA includes:

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard
* Preconfigured SSL certificates
* Pre-enabled system services

<img width="878" height="714" alt="system architecture drawio" src="https://github.com/user-attachments/assets/91d879f5-8303-4138-a493-1cd4f7188c72" />

___________________________________________________________________________________________________
<br>

## Lab Environment
### Host Machine
* 8GB RAM
* 512GB SSD
* Windows OS

### Virtual Machine Allocation
* 4GB RAM
* 2 CPU cores
* NAT networking
* Port Forwarding: 8443 → 443

___________________________________________________________________________________________________
<br>

⚖ OVA vs Manual Installation

| Feature | Manual Install | OVA Deployment |
|----------|----------|----------|
| Customization  | High   | Moderate   |
| Setup Time   | 30-60 mins   | 10-15 mins   |
| Complexity | Advanced | Beginner-Friendly |
|Use Case | Production builds | Lab & rapid deployment |

_____________________________________________________________________________________________________
<br>

## Skills Demonstrated

* Virtual appliance deployment
* NAT networking configuration
* Port forwarding
* Linux service management
* SIEM validation
* Technical documentation

_____________________________________________________________________________________________________
<br>

## Next Phase

This lab prepares the foundation for:<br>
* Multi-VM Home SOC lab
* Windows agent integration
* Attack simulation & detection
* Blue Team monitoring workflows

____________________________________________________________________________________________________
<br>

## Conclusion

The Wazuh OVA deployment provides a streamlined approach to SIEM lab setup. This method demonstrates appliance-based security deployment commonly used in enterprise and training environments.

This project represents a structured step toward building a full operational Home SOC lab.
