# Wazuh OVA – Installation and Setup Guide

Wazuh provides a pre-built virtual machine image in Open Virtual Appliance (OVA) format. It includes the Amazon Linux 2023 operating system and the Wazuh central components.

* Wazuh manager 4.14.3

* Filebeat-OSS 7.10.2

* Wazuh indexer 4.14.3

* Wazuh dashboard 4.14.3

You can import the Wazuh virtual machine image to VirtualBox or other OVA-compatible virtualization systems. This VM runs only on 64-bit systems with x86_64/AMD64 architecture. It does not provide high availability or scalability out of the box. However, you can implement these using distributed deployment.

## Step 1
### Download the OVA Image

* Visit the official [Wazuh download page](https://documentation.wazuh.com/current/deployment-options/virtual-machine/virtual-machine.html).

* Download the latest all-in-one OVA [virtual appliance (OVA)](https://packages.wazuh.com/4.x/vm/wazuh-4.14.3.ova) file.

* Verify file size (approx. 4–6GB).<br>

| OS | Architecture | VM Format | Version | Package |
|:---|:-------------:|:----------:|:--------:|--------:|
|Amazon Linux 2023 | 64-bit x86_64/AMD64 architecture | OVA | 4.14.3 | wazuh-4.14.3.ova (sha512) 

<br>

### Hardware requirements
The following requirements have to be in place before the Wazuh VM can be imported into a host operating system:

* The host operating system must be 64-bit with x86_64/AMD64 architecture.
* Enable hardware virtualization in the host firmware.
* Install a virtualization platform, such as VirtualBox, on the host system.

The Wazuh VM is configured with these specifications by default:

| Component | CPU (cores) | RAM (GB) | Storage (GB) |
|:----------|:-----------:|:--------:|-------------:|
| Wazuh v4.14.3 OVA | 4 | 8 | 50 |



The hardware configuration can be modified depending on the number of protected endpoints and indexed alert data. For more information about requirements, see [Quickstart](https://documentation.wazuh.com/current/quickstart.html).

<br>

## Step 2
### Import and access the virtual machine in VirtualBox
1. Import the [wazuh-4.14.3.ova](https://packages.wazuh.com/4.x/vm/wazuh-4.14.3.ova) file to your virtualization platform.
* Open VirtualBox.
* Click *"File → Import Appliance"*.
* Select the downloaded .ova file.
* Adjust hardware settings:
   * RAM: 4096MB
   * CPU: 2 cores
* Click Import.
<br>

2. If you use VirtualBox, set the Graphics Controller to *VMSVGA*. Other controllers can freeze the VM window.
* Select the imported VM
* Click *"Settings > Display"*
* Switch from Basic to Expert mode at the top-left of the settings window.
* From the Graphic controller dropdown, select the *VMSVGA* option.

<br>

## Step 3
### Configure Network Settings<br>
* Set Adapter to NAT

#### VirtualBox → Settings → Network → Adapter 1 → NAT

* Configure Port Forwarding

#### VirtualBox → Settings → Network → Advanced → Port Forwarding

| Name | Protocol |	Host | Port |	Guest | Port |
|:-----|:--------:|:----:|:----:|:-----:|-----:|
| Wazuh |	TCP | |	8443 | |	443 |

<br>

____________________________________________________________________________

## Step 4
### Start the Virtual Machine

* Start the VM.
* Allow full system initialization.
* Wait until login credentials are displayed on the console.

<img width="1920" height="1080" alt="OVA initialization" src="https://github.com/user-attachments/assets/e936f69f-345f-465f-a2b4-f1c51cc62f9e" />
<img width="1920" height="1080" alt="Root Login" src="https://github.com/user-attachments/assets/62280e3e-4244-416a-b6c8-a9c4d53871cb" />
<br>
<br>

* Log in using these credentials. You can use the virtualization platform or access it via SSH.
```bash
user: wazuh-user
password: wazuh
```
<br>
The SSH *root* user login is disabled. The *wazuh-user* has sudo privileges. To switch to root, execute the following command:
```bash
sudo -i
```
<br>
______________________________________________________________________________
<br>

## Step 5

Access the Wazuh dashboard
After starting the VM, access the Wazuh dashboard in a web browser using these credentials:

```bash
URL: https://<WAZUH_SERVER_IP> or https://localhost:8443
user: admin
password: admin
```
<br>

#### Note: If certificate warning appears:<br>
Click *"Advanced → Proceed"*
<br>

It might take a few seconds to minutes for the Wazuh dashboard to complete initialization. You can find *<WAZUH_SERVER_IP>* by typing the following command in the VM:

```bash
ip a
```
<br>
______________________________________________________________________________
<br>

## Step 6
### Validate Services

Inside the VM terminal:

```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
```

Expected output:
```bash
active (running)
```
_________________________________________________________________________________________________________________________________________________________________________________________
<br>

## Step 7
### Verify Resource Usage
```bash
htop
```
________________________________________________________________________________________________________________________________________________________________________________________________________________
<br>

## Configuration files
All components in this virtual image are configured to work out of the box. However, all components can be fully customized. These are the configuration file locations:

* Wazuh manager: /var/ossec/etc/ossec.conf

* Wazuh indexer: /etc/wazuh-indexer/opensearch.yml

* Filebeat-OSS: /etc/filebeat/filebeat.yml

* Wazuh dashboard:

    * /etc/wazuh-dashboard/opensearch_dashboards.yml

    * /usr/share/wazuh-dashboard/data/wazuh/config/wazuh.yml
<br>
_______________________________________________________________________________________________________________________________________________________________________
<br>

## VirtualBox time configuration
If you use VirtualBox, the VM might experience time skew when VirtualBox synchronizes the guest machine time. Follow the steps below to avoid this:

* Select the imported Wazuh VM
* Click on *"Settings > System"* 
* Switch from Basic to Expert mode at the top-left of the settings window.
* Click on the Motherboard sub-tab.
* Enable the *Hardware Clock in UTC Time* option under Features.

```bash
Note By default, the network interface type is set to Bridged Adapter. The VM attempts to obtain an IP address from the network DHCP server. Alternatively, you can set a static IP address by configuring the network files in Amazon Linux.
```
<br>

Once the virtual machine is imported and running, the next step is to [deploy the Wazuh agents](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html) on the systems to be monitored.
