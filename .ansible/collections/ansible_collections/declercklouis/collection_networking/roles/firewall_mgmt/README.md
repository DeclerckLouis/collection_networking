# firewall_mgmt

Manages firewall policies, address objects, and service objects on FortiGate and MikroTik devices.

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
| `firewall_policies` | list | List of firewall policy objects (see schema below) |
| `firewall_address_objects` | list | List of address objects used in policies |
| `firewall_service_objects` | list | List of custom service objects |

### Firewall policy object schema

```yaml
firewall_policies:
  - name: "ALLOW_MGMT_TO_SERVERS"   # Policy name
    src_zone: "MGMT"                 # Source zone/interface
    dst_zone: "SERVERS"              # Destination zone/interface
    src_address: "all"               # Source address object
    dst_address: "all"               # Destination address object
    service: "ALL"                   # Service or service group
    action: "accept"                 # accept | deny
    log: true                        # Enable logging
    state: "present"                 # present | absent
```

## Supported `ansible_network_os` values

| Vendor | `ansible_network_os` |
|--------|----------------------|
| FortiGate | `fortinet.fortios.fortios` |
| MikroTik | `community.routeros.api` |

## Example Playbook

```yaml
- hosts: firewalls
  gather_facts: false
  roles:
    - role: declercklouis.collection_networking.firewall_mgmt
      vars:
        firewall_policies:
          - name: "ALLOW_MGMT_TO_SERVERS"
            src_zone: "MGMT"
            dst_zone: "SERVERS"
            action: "accept"
            log: true
```

## License

GPL-3.0-or-later

## Author

Louis Declerck — [packetflow.be](https://lab.packetflow.be)
