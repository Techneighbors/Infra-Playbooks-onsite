# Dynamic Inventory Discovery Playbook

This playbook discovers active hosts in specified IP ranges and catalogs them into an Ansible inventory.

## Features

- Scans IP ranges using CIDR notation (e.g., 192.168.1.0/24)
- Discovers active hosts using ping
- Scans for common services (SSH, HTTP, HTTPS, RDP)
- Generates both YAML inventory and CSV report
- Automatically categorizes hosts by available services

## Usage

1. **Configure IP ranges** - Edit the `ip_ranges` variable in the playbook:

   ```yaml
   ip_ranges:
     - "192.168.1.0/24"
     - "192.168.2.0/24"
     - "10.0.0.0/24"
   ```

2. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

3. **Run the discovery**:
   ```bash
   ansible-playbook playbooks/simple-inventory-discovery.yml
   ```

## Output Files

- `inventory/discovered_hosts.yml` - Ansible inventory with discovered hosts
- `inventory/host_discovery_report.csv` - CSV report with service information

## Host Categories

The playbook automatically creates these host groups:

- `discovered_hosts` - All discovered active hosts
- `ssh_hosts` - Hosts with SSH (port 22) available
- `web_servers` - Hosts with HTTP (port 80) or HTTPS (port 443)
- `windows_hosts` - Hosts with RDP (port 3389) available

## Customization

You can modify these variables in the playbook:

- `ip_ranges` - List of IP ranges to scan (CIDR format)
- `service_ports` - Dictionary of services and ports to scan
- `timeout` - Timeout for each scan operation (seconds)
- `output_dir` - Directory for output files

## Example Output

```yaml
all:
  children:
    discovered_hosts:
      hosts:
        192.168.1.10:
          ansible_host: 192.168.1.10
          discovered_date: "2025-10-04T..."
          services:
            ssh: true
            http: true
        192.168.1.20:
          ansible_host: 192.168.1.20
          discovered_date: "2025-10-04T..."
          services:
            rdp: true
    ssh_hosts:
      hosts:
        192.168.1.10:
    web_servers:
      hosts:
        192.168.1.10:
    windows_hosts:
      hosts:
        192.168.1.20:
```

This allows you to target specific types of hosts in other playbooks using group names like `ssh_hosts` or `web_servers`.
