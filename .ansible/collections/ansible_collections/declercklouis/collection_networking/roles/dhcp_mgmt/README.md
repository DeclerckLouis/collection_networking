# dhcp_mgmt

Manages DHCP pools and static reservations on FortiGate and MikroTik devices.

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
| `dhcp_pools` | list | List of DHCP pool objects (see schema below) |

### DHCP pool object schema

```yaml
dhcp_pools:
  - name: MGMT_POOL              # Pool name
    vlan_id: 10                  # Associated VLAN ID
    subnet: "192.168.10.0/24"    # Subnet for the pool
    gateway: "192.168.10.1"      # Default gateway
    dns_servers:                 # DNS server(s)
      - "1.1.1.1"
      - "8.8.8.8"
    lease_time: 86400            # Lease duration in seconds
    reservations:                # Optional static reservations
      - mac: "AA:BB:CC:DD:EE:FF"
        ip: "192.168.10.10"
        hostname: "server01"
```

## Supported `ansible_network_os` values

| Vendor | `ansible_network_os` |
|--------|----------------------|
| FortiGate | `fortinet.fortios.fortios` |
| MikroTik | `community.routeros.api` |

## Example Playbook

```yaml
- hosts: network_devices
  gather_facts: false
  roles:
    - role: declercklouis.collection_networking.dhcp_mgmt
      vars:
        dhcp_pools:
          - name: MGMT_POOL
            subnet: "192.168.10.0/24"
            gateway: "192.168.10.1"
            dns_servers: ["1.1.1.1"]
```

## License

GPL-3.0-or-later

## Author

Louis Declerck — [packetflow.be](https://lab.packetflow.be)
