# Network Security Home Lab

## Overview

A hands-on network security lab demonstrating enterprise-style network segmentation, firewall policy design, NAT, VPN architecture, and packet-level traffic analysis.

The project combines security architecture documentation with practical Wireshark traffic analysis to demonstrate core Network Security Engineer skills.

## Skills Demonstrated

- Network segmentation and VLAN design
- Firewall security policy design
- Least-privilege access control
- Source NAT and Destination NAT
- Site-to-Site IPSec VPN concepts
- Remote-Access VPN concepts
- TCP/IP and DNS analysis
- Wireshark packet analysis
- HTTPS/TLS traffic analysis
- ICMP troubleshooting
- Security logging and monitoring

## Network Architecture

The lab separates user, server, and management systems into dedicated security zones.

                INTERNET
                    |
                FIREWALL
                    |
               CORE SWITCH
                    |
       ---------------------------
       |            |            |
    VLAN 10      VLAN 20      VLAN 30
     USERS        SERVERS     MANAGEMENT
       |            |            |
192.168.10.0/24 192.168.20.0/24 192.168.30.0/24

### Security Zones

| Zone | Network | Purpose |
|---|---|---|
| USERS | 192.168.10.0/24 | User endpoints |
| SERVERS | 192.168.20.0/24 | Internal services |
| MANAGEMENT | 192.168.30.0/24 | Administrative systems |
| UNTRUST | Internet | External networks |

## Security Controls

The lab applies several core network-security principles:

- Default-deny firewall policy
- Least-privilege access
- Network segmentation
- Management-network isolation
- Controlled Internet access
- Restricted inbound services
- NAT
- VPN encryption
- Security logging and monitoring

## Hands-On Traffic Analysis

Wireshark was used to capture and analyze network traffic generated during the lab.

### DNS Analysis

![DNS Analysis](screenshots/wireshark-dns.png)

DNS queries and responses were analyzed to identify domain-resolution behavior.

### HTTPS / TLS Analysis

![HTTPS Analysis](screenshots/wireshark-https.png)

TCP port 443 and TLS 1.3 traffic were examined to understand encrypted communication and connection metadata.

### ICMP Analysis

![ICMP Analysis](screenshots/wireshark-icmp.png)

ICMP echo requests and replies were captured to validate connectivity and demonstrate packet-level troubleshooting.

## Project Documentation

- [Network Architecture](diagrams/network-architecture.md)
- [Firewall Security Policies](firewall/firewall-rules.md)
- [NAT Configuration](firewall/nat-rules.md)
- [VPN Configuration](vpn/vpn-configuration.md)
- [Wireshark Traffic Analysis](monitoring/traffic-analysis.md)

## Tools & Technologies

**Networking:** TCP/IP, DNS, VLANs, ACLs, NAT  
**Security:** Firewall Policies, Network Segmentation, VPN, Least Privilege  
**VPN:** IPSec, Site-to-Site VPN, Remote-Access VPN  
**Monitoring:** Wireshark  
**Protocols:** DNS, TCP, TLS/HTTPS, ICMP

## Key Takeaways

This project demonstrates how network segmentation, firewall policies, NAT, VPN connectivity, and traffic monitoring can work together to protect an enterprise-style network.

The hands-on packet analysis demonstrates the ability to inspect network communication, apply protocol filters, troubleshoot connectivity, and identify traffic that may require further security investigation.

## Disclaimer

This project was created in an authorized lab environment for educational and portfolio purposes. IP addresses and configurations are examples used for documentation. No confidential company configurations, credentials, or production data are included.
