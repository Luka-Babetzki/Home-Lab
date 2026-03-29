# Home Lab

## Overview
A self-built home lab environment designed for hands-on security testing and research. Built to simulate a realistic enterprise network for practising offensive and defensive security techniques. Currently consists of an Active Directory domain running on VMware Workstation Pro, with a planned migration to a dedicated Proxmox bare-metal server.

## Asset Table

| Hostname |  Role                              | OS                     | IP                | 
|----------|------------------------------------|------------------------|-------------------|
| DC-01    |  Domain Controller (AD DS)         | Windows Server 2022    | 192.168.10.10/24  |
| WS-01    |  Target Machine                    | Windows 10             | 192.168.10.20/24  |
| KALI     |  Attacker Machine                  | Kali Linux             | 192.168.10.30/24  |


## Platform
VMware Workstation Pro

## Roadmap
- [ ] Create infrastructure diagram
- [ ] Add screenshots throughout documentation
- [ ] Migrate home lab setup from VMware to Proxmox

---

> **⚠️ Security Disclaimer:** This lab is an isolated environment built solely for educational purposes and authorised security testing. All activity is conducted within a private, self-contained network against systems I own and operate. Nothing documented here should be used against systems without explicit authorisation.