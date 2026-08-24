# Firewall Security Policies

## Overview

This section documents the firewall security policies used in the Network Security Home Lab.

The objective is to control communication between the USERS, SERVERS, MANAGEMENT, and UNTRUST security zones using least-privilege and default-deny principles.

## Security Zones

| Zone | Network | Purpose |
|---|---|---|
| UNTRUST | Internet | External network traffic |
| USERS | 192.168.10.0/24 | Employee/user devices |
| SERVERS | 192.168.20.0/24 | Internal servers |
| MANAGEMENT | 192.168.30.0/24 | Administrative systems |

## Firewall Policy Rules

| Rule | Source | Destination | Service | Action | Purpose |
|---|---|---|---|---|---|
| 1 | USERS | Internet | HTTP/HTTPS | ALLOW | Permit web browsing |
| 2 | USERS | Web Server | HTTPS/443 | ALLOW | Secure access to internal web server |
| 3 | USERS | DNS Server | DNS/53 | ALLOW | Permit DNS resolution |
| 4 | USERS | MANAGEMENT | ANY | DENY | Prevent users from accessing management systems |
| 5 | MANAGEMENT | SERVERS | SSH/HTTPS | ALLOW | Permit authorized administration |
| 6 | MANAGEMENT | Firewall | HTTPS/SSH | ALLOW | Permit firewall administration |
| 7 | Internet | USERS | ANY | DENY | Block unsolicited inbound traffic |
| 8 | Internet | MANAGEMENT | ANY | DENY | Protect management network |
| 9 | ANY | ANY | ANY | DENY | Default-deny all unauthorized traffic |

## Security Principles

### Least Privilege

Only traffic required for legitimate business or administrative purposes is permitted.

### Network Segmentation

Users, servers, and management systems are separated into different VLANs and security zones.

### Management Protection

The MANAGEMENT network cannot be accessed directly from the USERS or UNTRUST zones.

### Default Deny

Traffic that does not explicitly match an approved security policy is denied.

## Logging and Monitoring

Logging is enabled for security-relevant firewall rules.

Logs can be reviewed to identify:

- Denied connection attempts
- Suspicious source IP addresses
- Unauthorized access attempts
- Unusual traffic patterns
- Repeated connection failures

Security events can later be forwarded to a SIEM platform such as Splunk or Microsoft Sentinel for centralized monitoring and investigation.

## Testing

The following tests are used to validate the firewall policies:

1. Verify USERS can access HTTPS websites.
2. Verify USERS can reach the internal Web Server using HTTPS.
3. Verify USERS can query the authorized DNS Server.
4. Verify USERS cannot access the MANAGEMENT network.
5. Verify the Admin PC can securely access authorized servers.
6. Verify unsolicited Internet traffic cannot access internal networks.
7. Verify unauthorized traffic is blocked by the default-deny rule.

## Expected Result

Authorized communication should succeed while unauthorized communication between security zones should be blocked and logged.
