# VPN Configuration

## Overview

This section documents the VPN design used in the Network Security Home Lab.

The lab demonstrates two common enterprise VPN scenarios:

1. Site-to-Site IPSec VPN
2. Remote-Access VPN

VPN connectivity provides encrypted communication between trusted networks and authorized remote users.

---

## 1. Site-to-Site IPSec VPN

### Scenario

A site-to-site IPSec VPN connects the main office network to a remote branch network securely over the Internet.

### Network Design

Main Office:

192.168.10.0/24

        |
    [Firewall]
        |
     Internet
        |
    IPSec Tunnel
        |
    [Firewall]
        |
Remote Branch:

192.168.40.0/24

### Example Configuration

| Parameter | Main Office | Remote Branch |
|---|---|---|
| Local Network | 192.168.10.0/24 | 192.168.40.0/24 |
| Remote Network | 192.168.40.0/24 | 192.168.10.0/24 |
| VPN Type | IPSec | IPSec |
| IKE Version | IKEv2 | IKEv2 |
| Encryption | AES-256 | AES-256 |
| Integrity | SHA-256 | SHA-256 |
| DH Group | 14 | 14 |

> Note: Authentication secrets and production credentials are intentionally not included in this public repository.

---

## VPN Traffic Flow

User-PC
192.168.10.10

        |
        v

Main Firewall

        |
        | Encrypted IPSec Tunnel
        v

Remote Firewall

        |
        v

Branch Network
192.168.40.0/24

Traffic between the two networks is encrypted while traversing the external network.

---

## Firewall Policies

The VPN does not automatically allow unrestricted communication between sites.

Firewall policies are still used to control traffic.

| Source | Destination | Service | Action |
|---|---|---|---|
| Main Office | Branch Network | HTTPS | ALLOW |
| Main Office | Branch Network | DNS | ALLOW |
| Management | Branch Devices | SSH/HTTPS | ALLOW |
| Branch Network | Management | ANY | DENY |
| Any Unauthorized Traffic | Any | ANY | DENY |

This follows the principle of least privilege.

---

## 2. Remote-Access VPN

### Scenario

Remote-access VPN allows an authorized user to securely connect to internal resources from an external network.

### Traffic Flow

Remote User

        |
        v

     Internet

        |
        v

   VPN Gateway

        |
        v

Internal Resources

### VPN Address Pool

Example remote-user VPN pool:

10.10.50.0/24

Example assigned address:

10.10.50.10

---

## Remote-Access Security Controls

Remote VPN users should:

- Authenticate before receiving network access
- Receive an address from the dedicated VPN address pool
- Access only authorized internal resources
- Be restricted from sensitive management networks unless explicitly authorized
- Have VPN activity logged and monitored
- Use encrypted VPN communication

---

## Monitoring

VPN monitoring can include:

- Successful VPN connections
- Failed authentication attempts
- Tunnel establishment failures
- Unexpected source locations
- Repeated authentication failures
- Unusual VPN session activity
- Tunnel availability

Security-relevant VPN logs can be forwarded to a SIEM platform such as Splunk or Microsoft Sentinel.

---

## Testing

The following tests can be used to validate the VPN design:

1. Verify the site-to-site IPSec tunnel establishes successfully.
2. Verify the main office can reach authorized branch resources.
3. Verify unauthorized traffic between sites is blocked.
4. Verify remote users can establish a secure VPN connection.
5. Verify remote users receive an address from the VPN pool.
6. Verify remote users can access only approved internal resources.
7. Verify failed authentication attempts are logged.
8. Review firewall and VPN logs for connection activity.

---

## Expected Result

Authorized site-to-site and remote-access VPN traffic should establish securely while unauthorized communication remains blocked by firewall security policies.

## Security Note

All IP addresses, networks, and configuration values in this repository are part of a controlled lab design.

No production credentials, private keys, authentication secrets, or confidential company configurations are included.
