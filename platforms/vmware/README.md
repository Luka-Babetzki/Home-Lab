# Platform — VMware Workstation Pro

The current lab runs on VMware Workstation Pro, hosted on a personal machine. This is the initial platform before migration to a dedicated bare-metal Proxmox server.

---

## Host Machine

| Detail | Info |
|---|---|
| **Hypervisor** | VMware Workstation Pro 17.6 |
| **Host OS** | Windows 11 Home |
| **RAM** | 24GB |
| **CPU** | Intel Core i5 |
| **Storage** | 512GB SSD |

---

## Virtual Machines

| Hostname | OS | vCPUs | RAM | Disk |
|---|---|---|---|---|
| DC-01 | Windows Server 2022 | 2 | 4GB | 60GB |
| WS-01 | Windows 10 | 2 | 4GB | 60GB |
| KALI | Kali Linux | 2 | 4GB | 80GB |

**Minimum recommended host specs:** 16GB RAM, CPU with Intel VT-x or AMD-V enabled in BIOS, 200GB free disk space.

---

## Network Configuration

The lab operates on an isolated NAT network within VMware, preventing any unintended exposure to the host network.

| Detail | Info |
|---|---|
| **Type** | NAT (VMnet8) |
| **Subnet** | 192.168.10.0/24 |
| **Gateway** | 192.168.10.2 |
| **DNS** | 192.168.10.10 (DC-01) |

---

## Setup Guide

### 1. Install VMware Workstation Pro

1. Navigate to the [Broadcom Support Portal](https://support.broadcom.com)
2. Select VMware Workstation / Fusion Pro > Version 17.x
3. Download the installer for your host OS
4. Run the installer with default settings
5. Obtain a free licence key for personal/educational use

### 2. Download ISO Files

| OS | Source |
|---|---|
| Windows Server 2022 | [Microsoft Evaluation Centre](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022) |
| Windows 10 | [Microsoft Evaluation Centre](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise) |
| Kali Linux | [kali.org](https://www.kali.org/get-kali/#kali-virtual-machines) |

### 3. Create Virtual Machines

1. File > New Virtual Machine
2. Select **Typical (Recommended)**
3. Under "Installer disc image file (iso)", add the path to your ISO
4. Complete the setup wizard
5. Repeat for each VM

### 4. Configure NAT Network

1. In VMware: Edit > Virtual Network Editor
2. Verify VMnet8 (NAT) exists with subnet `192.168.10.0/24`
3. For each VM: Settings > Network Adapter > NAT

### 5. Configure Static IP Addresses

Assign each VM a static IP for consistency. DHCP is enabled by default but static addresses prevent IPs shifting between reboots.

| Hostname | Static IP |
|---|---|
| DC-01 | 192.168.10.10 |
| WS-01 | 192.168.10.20 |
| KALI | 192.168.10.30 |

### 6. Verify Connectivity

```bash
# From any VM, ping the others to confirm connectivity
ping 192.168.10.10
ping 192.168.10.20
ping 192.168.10.30
```

Verify each machine also has internet access via the NAT gateway.

---

## Troubleshooting

| Problem | Cause | Solution |
|---|---|---|
| Host unreachable when pinging Windows VMs | Windows Defender blocks ICMP by default | Create an inbound rule in Windows Defender Firewall to allow ICMPv4 |
| VM has no internet access | NAT not configured correctly | Verify VMnet8 exists and VM network adapter is set to NAT |

---

## Additional Resources

- [VMware Workstation Pro Documentation](https://docs.vmware.com/en/VMware-Workstation-Pro/)
- [VMware NAT Networking Guide](https://docs.vmware.com/en/VMware-Workstation-Pro/17/com.vmware.ws.using.doc/GUID-89311E3D-CCA9-4ECC-AF5C-C52BE6A89A95.html)