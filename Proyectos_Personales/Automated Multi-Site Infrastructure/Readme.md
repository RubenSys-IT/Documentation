Automated Multi-Site Infrastructure
This repository contains the Infrastructure as Code (IaC) automation using Ansible to deploy an interconnected multi-site network infrastructure. The design features a WireGuard Overlay tunnel and eBGP (FRR) dynamic routing across OPNsense firewalls.

📐 Architecture Overview
The project automates the provisioning and configuration of network components between two sites (HQ_Firewall and SedeB_Firewall) by directly interacting with the OPNsense REST API:

Secure Overlay (WireGuard):

Dynamic cryptographic key generation and public key derivation (wg genkey, wg pubkey).

Automated key exchange and peer registration between sites using runtime memory variables (hostvars).

Instantiation of the WireGuard service and kernel-level configuration reload.

Dynamic Routing (eBGP via FRR):

Automated enablement of the FRR (Free Range Routing) engine.

Configuration of local BGP parameters (ASN, Router ID, advertised networks).

Establishment of eBGP neighbor adjacencies across the WireGuard tunnel endpoints.

📁 Repository Structure
Plaintext
.
├── deploy_WireGuard.yml  # Playbook for deploying the encrypted Overlay tunnel
├── deploy_bgp.yml        # Playbook for provisioning eBGP via FRR REST API
└── README.md             # Main repository documentation
🚀 Prerequisites & Requirements
Control Node (Ansible)
Ansible Core >= 2.10

WireGuard CLI (wg) installed locally on the execution host for key generation.

ansible.builtin collection available.

OPNsense Instances
API Key and API Secret generated for an administrative user.

Installed plugins: os-frr and os-wireguard.

HTTPS API access enabled from the Ansible control node to the firewalls.

⚙️ Variables & Environment Setup
To run these playbooks securely, ensure you define your inventory (hosts.ini) and encrypted credentials file (group_vars/all/vault.yml).

Sample hosts.ini
Ini, TOML
[firewalls]
HQ_Firewall ansible_host=192.168.1.1
SedeB_Firewall ansible_host=192.168.2.1
Required Variables
opnsense_api_key & opnsense_api_secret

sedeB_api_key & sedeB_api_secret

bgp_asn, bgp_router_id, bgp_network

neighbor_ip, neighbor_asn, neighbor_description

hq_tunnel_address, sedeb_tunnel_address

🛠️ Usage
This documentation is licensed under CC BY-NC-ND 4.0:

Attribution (BY): You must give credit to the author (R. Rubén).

Non-Commercial (NC): You may not use this material for commercial purposes.

No Derivatives (ND): You may not modify or distribute derivative works.

You are free to read, study, and share this documentation for educational purposes only, as long as you comply with the license terms.

⚠️ Disclaimer
This documentation is for educational purposes only.

Any third-party software mentioned (e.g., Wazuh, VMware) is not included and must be obtained legally.

The author is not responsible for any misuse of this material.

Screenshots, guides, and configuration instructions are provided solely as learning references.

Certain sensitive details have been omitted or censored for safety purposes. This documentation is intended for educational use only.