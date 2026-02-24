# Wazuh OVA Deployment – Troubleshooting Guide
## 1️. Dashboard Not Accessible

Issue:<br>
https://localhost:8443 not loading

###  Possible Causes

* Port forwarding misconfigured
* Dashboard service not running
* Wrong host port

### Verify Dashboard Service
```bash
sudo systemctl status wazuh-dashboard
```

If inactive:
```bash
sudo systemctl restart wazuh-dashboard
```
<br>
________________________________________________________________________________________


## 2. Services Not Running
```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
```

Restart:
```bash
sudo systemctl restart wazuh-manager
sudo systemctl restart wazuh-indexer
sudo systemctl restart wazuh-dashboard
```
<br>
______________________________________________________________________________________________________________


## 3️. High Memory Usage

Check usage:
```bash
htop
```

Solutions:

* Increase RAM to 6GB
* Close host applications
* Reduce background services

<br>
____________________________________________________________________________________________________________________


## 4️. Port Already in Use
```bash
sudo lsof -i :443
```

Stop conflicting service or change port mapping.

<br>
_______________________________________________________________________________________________________________________


## 5️. Certificate Warning

Self-signed certificate is expected.<br>

Click:<br>

#### Advanced → Proceed

For production, install valid SSL certificate.

<br>
___________________________________________________________________________________________________________________________

## 6. VM fails to start on AMD processors with VMware
### Issue:<br>

* After importing the Wazuh OVA into VMware Workstation on a host with an AMD processor, the VM fails to start with the error:

```bash
The guest operating system has disabled the CPU. Power off or reset the virtual machine.
```

### Workaround:

a. Locate and edit the VM *< .vmx >* file after importing the OVA.

b. Add the following lines to the end of the file to resolve compatibility issues between the VM and AMD processors.

```bash
cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
featureCompat.enable = "FALSE"
```

c. Save the file and power on the VM.

<br>

## Upgrading the VM
The virtual machine can be upgraded as a traditional installation:

[Upgrading the Wazuh central components](https://documentation.wazuh.com/current/upgrade-guide/upgrading-central-components.html)
