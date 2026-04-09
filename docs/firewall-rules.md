# Firewall Rules

## Philosophy

The firewall policy is based on a **default deny** model. Inter-VLAN traffic is blocked unless there is a clearly defined requirement for access.

This reduces the attack surface and prevents unrestricted east-west traffic inside the lab.

## Default Rules

- deny all traffic between VLANs by default
- allow only explicit, documented exceptions
- restrict management access to approved administrative systems
- permit outbound traffic only where required

## Rule Strategy by Zone

### Management VLAN

#### Allowed

- management workstation to pfSense web interface
- management workstation to Proxmox web interface
- SSH from approved administrative systems
- DNS and NTP as needed

#### Denied

- broad inbound access from DMZ / IoT
- unnecessary access from general trusted clients

### Trusted LAN VLAN

#### Allowed

- internet access for standard outbound traffic
- DNS to approved resolver
- limited access to management services where justified
- access to internal services hosted in trusted zones

#### Denied

- unrestricted access to management infrastructure
- unnecessary administrative ports

### DMZ / IoT VLAN

#### Allowed

- internet access if required
- DNS to approved resolver
- access only to explicitly published internal services if needed

#### Denied

- access to Management VLAN
- unrestricted access to Trusted LAN
- administrative access to Proxmox or pfSense

## Example Policy Matrix

| Source | Destination | Action | Reason |
|--------|-------------|--------|--------|
| Management VLAN | pfSense / Proxmox | Allow | Administrative access |
| Trusted LAN | Internet | Allow | Standard outbound use |
| Trusted LAN | Management VLAN | Limited Allow | Approved admin-only access |
| DMZ / IoT | Internet | Allow | Device functionality |
| DMZ / IoT | Trusted LAN | Deny | Prevent lateral movement |
| DMZ / IoT | Management VLAN | Deny | Protect admin plane |

## Security Rationale

A compromised IoT device or public-facing VM should not be able to:

- discover administrative interfaces
- access hypervisor management
- move into trusted user networks
- establish unrestricted connections to internal resources

## Operational Notes

Firewall rules should be reviewed whenever:

- a new VM is deployed
- a new VLAN is introduced
- a service is exposed externally
- a device changes trust level

Rules should remain as narrow as possible by limiting:

- source network
- destination IP
- protocol
- destination port
