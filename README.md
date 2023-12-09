ebdruplab.keepalived
=========

Ansible Role: ebdruplab.keepalived

This role installs and configures Keepalived for high availability and load balancing solutions. It supports both RedHat and Debian based systems.

Requirements
------------

No specific requirements. This role relies on features provided by Ansible itself and does not require any external dependencies. Ensure that your system has Ansible installed.

Role Variables
--------------

The role uses the following variables which are set in `defaults/main.yml`:

- `ebdruplab_keepalived_service_user`: User for running Keepalived scripts.
- `ebdruplab_keepalive_service_mon_name`: Name of the service to monitor
- `ebdruplab_keepalived_service_mon_port`: The port number on witch to check monitor
- `ebdruplab_keepalived_service_group`: Group for running Keepalived scripts.
- `ebdruplab_keepalived_vrrp_script`: Configuration details for the VRRP script, including script location, run interval, and run weight.
- `ebdruplab_keepalived_config`: General configuration for Keepalived, including NIC, state (MASTER or BACKUP), virtual router ID, priority, and advertisement interval.
- `ebdruplab_keepalived_auth_pass`: Password for VRRP authentication.
- `ebdruplab_keepalived_unicast`: Boolean to enable unicast. Defaults to `false`.
- `ebdruplab_keepalived_primary_ip`: Primary IP for unicast.
- `ebdruplab_keepalived_backup_ip`: Backup IP for unicast.
- `ebdruplab_keepalived_virtual_ip`: Virtual IP address.

```yaml
# Examples
# User and group for Keepalived scripts
ebdruplab_keepalived_service_user: "keepalived_user"
ebdruplab_keepalived_service_group: "keepalived_user"

# monitor
ebdruplab_keepalive_service_mon_name: httpd
ebdruplab_keepalived_service_mon_port: 443

# Configuration for VRRP script
ebdruplab_keepalived_vrrp_script:
  script_location: "/etc/keepalived/scripts/chk_health.sh" # Adjust the script location as necessary
  run_interval: 2 # Interval in seconds for running the health check script
  run_weight: 2 # Weight adjustment for the script

# Configuration for the Keepalived service
ebdruplab_keepalived_config:
  keepalived_nic: "eth0" # Network interface for Keepalived
  keepalived_state: "MASTER" # or "BACKUP"
  virtual_router_id: 51 # Virtual router ID
  keepalived_priority: 100 # Priority for VRRP
  advert_int: 1 # Advertisement interval

# Authentication information for VRRP
ebdruplab_keepalived_auth_pass: "your_secret_pass"

# Unicast configuration - set to true if unicast is used instead of multicast
ebdruplab_keepalived_unicast: false
ebdruplab_keepalived_primary_ip: "192.168.1.1" # Primary IP for unicast
ebdruplab_keepalived_backup_ip: "192.168.1.2" # Backup IP for unicast
ebdruplab_keepalived_virtual_ip: "192.168.1.100" # Virtual IP address
```

Dependencies
------------

No other Galaxy roles are required.

Example Playbook
----------------

Here is an example of how to use this role:

```yaml
- hosts: servers
  become: true
  roles:
    - { role: ebdruplab.keepalived }
