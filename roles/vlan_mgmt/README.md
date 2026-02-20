# vlan_mgmt

Manages VLANs across FortiGate, MikroTik, and Ubiquiti UniFi devices.

## Requirements

The following Ansible collections must be installed:

```
fortinet.fortios
community.routeros
```

Install them via:
```bash
ansible-galaxy collection install -r requirements.yml
```

## Role Variables

All variables are expected to be delivered by the **NetBox dynamic inventory** in production.
Defaults in `defaults/main.yml` are for local testing/syntax-checks only.

| Variable | Type | Description |
|----------|------|-------------|
| `vlans` | list | List of VLAN objects (see schema below) |

### VLAN object schema

```yaml
vlans:
  - id: 10                          # VLAN ID (integer)
    name: MGMT                      # Human-readable name
    description: "Management VLAN"  # Optional
    ipv4_prefix: "192.168.10.0/24"  # Optional
    ipv6_prefix: "fd00:10::/64"     # Optional
```

## Supported `ansible_network_os` values

| Vendor | `ansible_network_os` |
|--------|----------------------|
| FortiGate | `fortinet.fortios.fortios` |
| MikroTik | `community.routeros.api` |
| Ubiquiti UniFi | *(TBD — UniFi API)* |

## Example Playbook

```yaml
- hosts: network_devices
  gather_facts: false
  roles:
    - role: declercklouis.collection_networking.vlan_mgmt
      vars:
        vlans:
          - id: 10
            name: MGMT
            ipv4_prefix: "192.168.10.0/24"
```

## License

GPL-3.0-or-later

## Author

Louis Declerck — [packetflow.be](https://lab.packetflow.be)
