# NAT Configuration

## Overview

This section documents the Network Address Translation (NAT) design used in the Network Security Home Lab.

NAT allows internal private networks to communicate with external networks while keeping internal IP addressing hidden from the Internet.

## NAT Types Used

### Source NAT

Source NAT is used when internal devices access the Internet.

Example:

User-PC:

192.168.10.10

↓

Firewall performs Source NAT

↓

Public IP:

203.0.113.10

This allows internal systems using private IP addresses to communicate with external services through the firewall.

## Source NAT Rules

| Rule | Source Zone | Source Network | Destination | Translation | Action |
|---|---|---|---|---|---|
| SNAT-01 | USERS | 192.168.10.0/24 | Internet | Firewall Public IP | Allow |
| SNAT-02 | SERVERS | 192.168.20.0/24 | Internet | Firewall Public IP | Allow |
| SNAT-03 | MANAGEMENT | 192.168.30.0/24 | Internet | Firewall Public IP | Restricted |

## Destination NAT

Destination NAT can be used when an approved internal service needs to be accessible from an external network.

Example:

External Client

↓

203.0.113.20:443

↓

Firewall DNAT

↓

Web Server

192.168.20.10:443

## Destination NAT Rule

| Rule | Source | Public Destination | Internal Destination | Service | Action |
|---|---|---|---|---|---|
| DNAT-01 | Internet | 203.0.113.20 | 192.168.20.10 | HTTPS/443 | Allow |

Only HTTPS traffic is permitted to the web server.

Direct external access to the USERS and MANAGEMENT networks remains blocked.

## Security Considerations

NAT alone is not treated as a security control.

Corresponding firewall security policies are required to permit authorized traffic.

Security controls include:

- Restrict inbound traffic to required services
- Do not expose the management network to the Internet
- Limit server exposure to approved ports
- Log inbound connections
- Apply least-privilege firewall policies
- Deny unauthorized inbound traffic

## Testing

The following tests can be used to validate the NAT configuration:

1. Verify a USERS host can access the Internet.
2. Confirm the private source IP is translated by the firewall.
3. Verify the Web Server can be reached externally only through HTTPS.
4. Verify unauthorized ports to the Web Server are blocked.
5. Verify the MANAGEMENT network cannot be accessed directly from the Internet.
6. Review firewall logs to confirm NAT and security policy behavior.

## Expected Result

Internal systems should access approved external resources through Source NAT.

Only explicitly approved services should be reachable through Destination NAT, while unauthorized inbound traffic remains blocked.
