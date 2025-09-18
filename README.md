# MATLAB Ansible Installer

Ansible playbook and role for installing MATLAB on Ubuntu 22.04 and RHEL8 workstations in secure, airgapped environments with STIG compliance.

## Overview

This Ansible solution provides automated MATLAB installation for x86_64 workstations in secure, airgapped environments. It includes comprehensive security controls, audit logging, and compliance features required for government and enterprise deployments.

## Features

- **Multi-OS Support**: Ubuntu 22.04 and RHEL8 distributions
- **Security Compliance**: STIG-compliant configurations, SELinux/AppArmor integration
- **Airgapped Environment**: Offline installation with local repositories
- **Audit Logging**: Comprehensive logging for compliance and troubleshooting
- **Silent Installation**: Automated, unattended MATLAB deployment
- **Network Licensing**: Support for license servers in airgapped networks
- **Installation Profiles**: Standard (17 toolboxes) or Full (100+ toolboxes)

## Quick Start

1. **Configure license settings**:
   ```bash
   vim roles/matlab-installer/defaults/main.yml
   # Update matlab_license_server, matlab_license_port, matlab_file_installation_key
   ```

2. **Update inventory**:
   ```bash
   vim inventory/hosts.yml
   ```

3. **Stage MATLAB installer**:
   - Copy MATLAB installer to `/opt/software/matlab/`
   - Copy documentation to `/opt/software/matlab/documentation/` (optional)

4. **Run the playbook**:
   ```bash
   ansible-playbook -i inventory/hosts.yml install-matlab-linux.yml
   ```

## Configuration

### Required Configuration Variables

Edit `roles/matlab-installer/defaults/main.yml`:

```yaml
matlab_license_server: "license.example.local"
matlab_license_port: "27000"
matlab_file_installation_key: "YOUR_INSTALLATION_KEY"
```

Edit `group_vars/all.yml`:

```yaml
ansible_user: "ansible"
ansible_ssh_private_key_file: "~/.ssh/id_rsa"
```

### Installation Profiles

- **Standard Profile**: 17 essential toolboxes for most engineering work
- **Full Profile**: All 100+ available toolboxes (default)

Set profile: `matlab_installation_profile: "standard"` or `"full"`

### Key Options

```yaml
matlab_version: "R2025a"                    # MATLAB version
matlab_installation_profile: "full"         # Standard or full installation
matlab_install_documentation: true          # Include documentation
matlab_create_desktop_shortcuts: true       # Create desktop shortcuts
```

## System Requirements

- x86_64 workstations
- Ubuntu 22.04 LTS or RHEL8
- Minimum 25GB disk space
- Minimum 4GB RAM
- Ansible 2.12 or later

## Directory Structure

```
ansible-matlab-installer/
├── install-matlab-linux.yml          # Main playbook
├── roles/matlab-installer/            # MATLAB installer role
├── group_vars/                        # Group variables
│   ├── all.yml                       # Global variables
│   └── matlab_workstations.yml       # Workstation-specific variables
└── inventory/hosts.yml               # Main inventory
```

## License

This project is proprietary and intended for internal use in secure government and enterprise environments.

## Support

For issues:
- Check logs in `/var/log/matlab/` and `/var/log/ansible/`
- Contact your system administrator or IT security team