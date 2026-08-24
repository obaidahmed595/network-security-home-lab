# Network Architecture

## Overview

This lab uses a segmented enterprise-style network architecture designed to separate user, server, and management traffic.

## Network Design

                 INTERNET
                    |
                [FIREWALL]
                    |
               [CORE SWITCH]
                    |
        ---------------------------
        |            |            |
     VLAN 10      VLAN 20      VLAN 30
      USERS        SERVERS     MANAGEMENT
        |            |            |
 192.168.10.0/24 192.168.20.0/24 192.168.30.0/24


## VLAN and IP Addressing

| VLAN | Zone | Network | Gateway |
|------|------|---------|---------|
| VLAN 10 | USERS | 192.168.10.0/24 | 192.168.10.1 |
| VLAN 20 | SERVERS | 192.168.20.0/24 | 192.168.20.1 |
| VLAN 30 | MANAGEMENT | 192.168.30.0/24 | 192.168.30.1 |

## Example Hosts

| Device | VLAN | IP Address |
|--------|------|------------|
| User-PC | VLAN 10 | 192.168.10.10 |
| Web-Server | VLAN 20 | 192.168.20.10 |
| DNS-Server | VLAN 20 | 192.168.20.20 |
| Admin-PC | VLAN 30 | 192.168.30.10 |

## Security Design

The network is segmented to reduce unnecessary communication between systems.

Key security principles include:

- Separation of users, servers, and management systems
- Firewall-controlled communication between security zones
- Restricted access to the management network
- Least-privilege access between network segments
- Default-deny policy for unauthorized traffic
- Controlled Internet access through firewall policies and NAT
