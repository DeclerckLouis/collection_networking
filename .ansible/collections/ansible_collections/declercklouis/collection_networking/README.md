# Ansible Collection  
## `declercklouis.collection_networking`

A collection used to automate network configuration in the **Packetflow homelab**.
Manages FortiGate, MikroTik, and Ubiquiti UniFi devices via [NetBox](https://netbox.dev) as the single Source of Truth and [AWX](https://github.com/ansible/awx) for execution.

> **Notice:** This collection is under active development. Use at your own risk.

## Roles

| Role | Description |
|------|-------------|
| [`vlan_mgmt`](roles/vlan_mgmt/README.md) | Create and manage VLANs |
| [`dhcp_mgmt`](roles/dhcp_mgmt/README.md) | Manage DHCP pools and static reservations |
| [`firewall_mgmt`](roles/firewall_mgmt/README.md) | Manage firewall policies and objects |

## Supported Vendors

- **FortiGate** (`fortinet.fortios`)
- **MikroTik** (`community.routeros`)
- **Ubiquiti UniFi** *(planned)*

## Requirements

- Ansible Core >= 2.16
- Python >= 3.10

Install collection dependencies:

```bash
ansible-galaxy collection install -r requirements.yml
```

## Usage

```yaml
# Example playbook
- hosts: network_devices
  gather_facts: false
  collections:
    - declercklouis.collection_networking
  roles:
    - vlan_mgmt
    - dhcp_mgmt
```

## Architecture

This collection uses `tasks/main.yml` in each role to route execution to vendor-specific task files based on `ansible_network_os`.  
All variable data is sourced from NetBox via the dynamic inventory plugin — no hardcoded values.  

## License

GPL-3.0-or-later

## Author

Louis Declerck — [packetflow.be](https://lab.packetflow.be) · [GitHub](https://github.com/declercklouis/collection-networking)