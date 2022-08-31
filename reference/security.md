Good inventory management hygene: No unknown servers on infra
MFA on servers
Use SSH private keys instead of passwords
Bastion/Jump Host for access to critical infra
Firewall with deny all default and only open as required (e.g. no SSH/RDP accessible to the Internet, instead jump through a MFA enabled VPN first)
Include info on IP based DDoS and how to mitigate it
Engine API being filtered + auth for Engine API
VLAN Segmentation
OS hardening (this involves quite a few things, but https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-123.pdf provides quite a lot of details and there are playbooks that will do a lot of it)
EDR, SIEM, NDR and when to use them?
