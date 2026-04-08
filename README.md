# Home Lab Cybersecurity: Zero Trust Network Architecture

## Overview

This project documents the design and implementation of a segmented home lab environment using **pfSense** and **Proxmox VE**. The objective is to improve the overall security posture of the lab by applying **Zero Trust principles**, **network segmentation**, **least privilege access control**, and **layered defense**.

Rather than operating on a flat network, this lab isolates management systems, trusted clients, and higher-risk devices into separate security zones using VLANs and firewall enforcement. The project simulates enterprise-style network security controls in a personal lab setting and demonstrates practical cybersecurity engineering skills.

## Goals

- Eliminate flat network architecture
- Reduce lateral movement opportunities
- Protect management interfaces from untrusted devices
- Enforce least privilege with inter-VLAN firewall rules
- Add visibility through IDS/IPS monitoring
- Secure remote access without exposing internal management services

## Environment

- **Firewall/Router:** pfSense
- **Hypervisor:** Proxmox VE
- **Virtual Networking:** Linux bridges and VLAN-aware configuration
- **Remote Access:** VPN
- **Detection/Monitoring:** Suricata IDS/IPS

## Security Design

The lab is segmented into dedicated network zones:

- **Management VLAN**
  - Used for administrative access to pfSense, Proxmox, and other infrastructure services
- **Trusted LAN VLAN**
  - Used for daily-use endpoints and trusted internal systems
- **DMZ / IoT VLAN**
  - Used for higher-risk devices, public-facing services, and isolated workloads

Traffic between VLANs is blocked by default and only explicitly approved flows are permitted.

## Architecture Diagram

```mermaid
flowchart TD
    A[Internet] --> B[pfSense Firewall]
    B --> C[Management VLAN]
    B --> D[Trusted LAN VLAN]
    B --> E[DMZ / IoT VLAN]

    C --> F[Proxmox Management]
    C --> G[Infrastructure Services]

    D --> H[Trusted Endpoints]
    D --> I[Internal VMs]

    E --> J[IoT Devices]
    E --> K[Public-Facing Services]

    E -. blocked .-> C
    E -. blocked .-> D
