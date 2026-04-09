# IDS/IPS with Suricata

## Purpose

Suricata provides network visibility and threat detection for the lab by inspecting traffic for suspicious or malicious activity. This adds a monitoring and prevention layer beyond static firewall rules.

## Why It Matters

Firewall rules control what should be allowed. IDS/IPS helps detect when permitted traffic is being abused or when known attack patterns appear on the network.

## Deployment Goals

- inspect traffic entering and leaving sensitive segments
- identify scanning, exploitation attempts, and suspicious behavior
- improve visibility into lab traffic patterns
- support future expansion into centralized logging or alerting

## Benefits

- detects common malicious signatures
- supports prevention mode where appropriate
- provides additional evidence during testing or incident review
- strengthens layered defense in the environment

## Tuning Considerations

IDS/IPS requires tuning to avoid excessive noise and false positives.

Important practices include:

- starting with alerting before aggressive blocking
- reviewing triggered signatures
- suppressing clearly benign noise
- tuning policy to match actual lab usage

## Example Use Cases

- detecting port scans from a compromised device
- identifying suspicious outbound connections
- alerting on exploit attempts against exposed services
- validating segmentation effectiveness during testing

## Security Outcome

Suricata helps move the lab from simple network connectivity into active defensive monitoring, which better reflects real-world cybersecurity operations.
