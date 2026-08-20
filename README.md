# Network Security Home Lab

## Overview

This project demonstrates a simulated enterprise network security environment focused on firewall configuration, VLAN segmentation, VPN connectivity, access control, traffic monitoring, and basic security testing.

The goal of this lab is to demonstrate practical network security concepts using technologies and workflows commonly used by Network Security Engineers.

## Objectives

- Design a segmented network architecture
- Configure firewall security policies
- Implement VLAN-based network segmentation
- Configure NAT and ACL rules
- Demonstrate site-to-site and remote-access VPN concepts
- Monitor network traffic
- Analyze suspicious network activity
- Document security configurations and findings

## Technologies

- Palo Alto Firewall
- Fortinet / FortiGate
- Cisco Routers & Switches
- Wireshark
- TCP/IP
- DNS
- VLANs
- ACLs
- NAT
- IPSec VPN
- SSL VPN

## Lab Architecture

Planned architecture:

Internet
   |
Firewall
   |
Core Router / Switch
   |
---------------------------------
|               |               |
VLAN 10         VLAN 20         VLAN 30
Users           Servers         Management
192.168.10.0    192.168.20.0    192.168.30.0
/24             /24             /24

## Security Controls

The lab includes:

- Firewall policy configuration
- Network segmentation
- ACL implementation
- NAT configuration
- VPN connectivity
- IDS/IPS monitoring
- Traffic analysis using Wireshark
- Restricted communication between VLANs

## Project Structure

network-security-home-lab/

- README.md
- diagrams/
- firewall/
- vpn/
- monitoring/
- screenshots/

## Future Improvements

- Add SIEM integration
- Add centralized logging
- Add IDS/IPS detection scenarios
- Integrate AWS or Azure network security
- Automate configuration checks using Python

## Disclaimer

This project is created in a controlled lab environment for educational and portfolio purposes. No production systems or unauthorized networks are used.
