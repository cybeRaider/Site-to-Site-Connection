# Enterprise-Grade Site-to-Site IKEv2 IPsec VPN & Monitoring Lab

## Overview
This repository documents the architecture and implementation of a secure, segmented Site-to-Site IKEv2 IPsec VPN tunnel established between an Ubuntu Server 24.04 endpoint that is etsablsihed on Raspberry Pi (running StrongSwan) and a pfSense Firewall appliance. 

## Core Technologies & Tools
- Operating Systems: Ubuntu Server 24.04 LTS, pfSense CE, Ubuntu Desktop (LAN Client)
- Hypervisor: VMware (Type-2 Hypervisor environment)
- VPN Daemon: StrongSwan (Charon IKE daemon).
- Security & Encryption: OpenSSL (Custom CA & Certificate Generation), IKEv2, Mutual RSA, AES-256-GCM / SHA256.
- Monitoring: Zabbix Server

## Network Architecture & Topology

To mirror enterprise best practices, the Ubuntu Server utilizes a dedicated virtual loopback/dummy interface ("dummy0"). This ensures that home network traffic remains fully isolated and only explicit, segmented traffic passes through the encrypted tunnel.

Ubuntu Server -> (Lab WAN: 192.168.X.X)
  - dummy interface -> [Subnet: 10.X.X.X] and IP Interface: dummy0 (10.X.X.X)                   
  
pfSense Firewall -> [WAN Interface: 192.168.X.X], [DMZ Interface: 172.16.X.X], [LAN Subnet: 192.168.X.X] 
  
IPsec Connection is between the dummy interface and Ubuntu Desktop VM in LAN interface of pfsense.                                                         
