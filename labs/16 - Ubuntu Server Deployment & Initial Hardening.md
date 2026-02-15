# Ubuntu Server Deployment & Initial Hardening

## Objective

Deploy a headless Ubuntu Server virtual machine and configure it for secure remote administration. Validate networking, SSH access, firewall configuration, and system updates.

This lab establishes the foundational infrastructure that will support future services such as DNS, web hosting, mail services, logging, and synchronization.

---

## Environment

- Host Platform: VMware Workstation
- Client VM: Ubuntu Desktop
- Server VM: Ubuntu Server (LTS)
- Network Mode: NAT (DHCP assigned)
- Resources:
  - 2 vCPUs
  - 2–4 GB RAM
  - 20+ GB disk

---

## Installation Overview

### 1. Ubuntu Server ISO Installation
- Used latest LTS release
- Selected automatic storage configuration
- Configured hostname (e.g., `lab-server`)
- Created standard non-root user
- Installed OpenSSH Server during setup

---

## Network Validation

After installation:

ip a
Confirmed DHCP-assigned IP address

ping google.com
Verified:
- DNS resolution
- External connectivity

System Update

Updated package lists and upgraded installed packages:

sudo apt update && sudo apt upgrade -y

Ensured system was current before deploying services.

Firewall Configuration (UFW)

Enabled uncomplicated firewall:
sudo ufw enable
sudo ufw status

Allowed SSH traffic:

sudo ufw allow ssh


Confirmed:
- Firewall active
- SSH allowed
- Default deny incoming policy in place
- SSH Validation

From Ubuntu Desktop VM:

ssh username@server-ip

Validated:
- Remote connectivity
- OpenSSH service running
- Credential authentication working
- Firewall not blocking access

Verified SSH service status:

sudo systemctl status ssh

Confirmed service active and enabled.

---

## Key Takeaways

- Headless systems require comfort with CLI management.
- SSH is foundational for remote infrastructure administration.
- Enabling a firewall early prevents accidental exposure.
- Validating connectivity (IP, DNS, outbound traffic) is critical before deploying services.
- Proper baseline configuration reduces future troubleshooting complexity.

---

## Future Enhancements

- Implement SSH key-based authentication
- Disable password authentication
- Configure static IP addressing
- Apply additional system hardening

This server will serve as the infrastructure foundation for subsequent labs involving DNS, web services, mail services, logging, and synchronization.
