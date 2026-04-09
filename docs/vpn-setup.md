# Secure Remote Access

## Objective

Remote administrative access should be secured without exposing internal management interfaces directly to the internet.

The preferred approach is to require a VPN before any access to internal infrastructure is permitted.

## Security Approach

Administrative services such as:

- pfSense web UI
- Proxmox web UI
- SSH access to infrastructure

should not be published through direct port forwarding.

Instead, users connect through a VPN and then access internal services from the secured internal network.

## Benefits

- reduces internet-facing attack surface
- prevents direct exposure of administrative ports
- adds authentication before network access is granted
- supports controlled access into specific VLANs

## Recommended Access Model

1. establish VPN connection
2. authenticate with approved credentials
3. permit access only to required management subnets
4. log or monitor remote access attempts where possible

## Good Practices

- restrict VPN users to only required subnets
- use strong credentials and key-based authentication where available
- disable unused VPN accounts
- review remote access logs periodically
- avoid sharing administrative accounts

## Security Outcome

Using VPN-based administrative access helps protect the most sensitive parts of the environment while preserving the ability to securely manage the lab from outside the home network.
