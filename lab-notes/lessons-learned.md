# Lessons Learned

## Flat Networks Create Unnecessary Risk

Operating on a flat network makes it easier for a compromised device to enumerate systems and move laterally. Segmentation significantly improves containment.

## Management Traffic Must Be Isolated

Administrative interfaces should live on a dedicated network and should not be accessible from general-purpose or higher-risk devices.

## Default Deny Is Easier to Secure

Starting from a deny-all posture makes it easier to reason about access and creates fewer accidental exposures.

## Security Monitoring Requires Tuning

IDS/IPS tools are useful, but they require tuning to be operationally valuable. Too much noise reduces effectiveness.

## Remote Access Should Be Intentional

Exposing management services directly to the internet increases risk. VPN access is a much stronger model for secure administration.

## Small Labs Still Benefit from Enterprise Practices

Even in a home lab, concepts like segmentation, least privilege, and layered defense are practical and measurable improvements.
