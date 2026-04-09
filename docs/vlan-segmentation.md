# VLAN Segmentation Strategy

## Overview

This lab uses VLANs to isolate systems by trust level and administrative purpose. Segmentation is one of the most effective ways to improve security in a home lab because it limits direct communication between unrelated devices and reduces the impact of compromise.

## VLAN Plan

| VLAN | Name | Purpose | Example Subnet |
|------|------|---------|----------------|
| 10 | Management | Administrative access to infrastructure | 10.10.10.0/24 |
| 20 | Trusted LAN | Trusted clients and internal systems | 10.10.20.0/24 |
| 30 | DMZ / IoT | High-risk or isolated systems | 10.10.30.0/24 |

## Rationale

### VLAN 10 - Management

This network is reserved for infrastructure administration. It contains systems that should never be exposed to untrusted segments.

Examples:

- Proxmox management IP
- pfSense administrative access
- monitoring systems
- backup infrastructure

### VLAN 20 - Trusted LAN

This segment is for trusted user endpoints and internal lab systems that require internet access and may need controlled access to management resources.

Examples:

- workstation
- laptop
- internal service VMs
- administrative jump host

### VLAN 30 - DMZ / IoT

This segment contains devices or services that carry greater risk and should not be allowed to directly reach management systems or trusted endpoints.

Examples:

- IoT devices
- experimental VMs
- public-facing services
- sandbox systems

## Security Policy Summary

- VLAN 10 should not be broadly reachable from other VLANs
- VLAN 20 may access specific services in VLAN 10 if required
- VLAN 30 must not initiate traffic to VLAN 10
- VLAN 30 must not freely communicate with VLAN 20
- all internet-bound traffic is routed through pfSense and filtered according to policy

## Benefits of Segmentation

- limits lateral movement
- protects administrative services
- improves visibility of traffic flows
- makes firewall policy easier to reason about
- creates cleaner security boundaries for future expansion
