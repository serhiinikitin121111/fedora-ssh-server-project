# Installation Guide

This document provides a complete step-by-step installation and setup guide for preparing the Fedora Linux virtual machine for remote access using SSH.  
The instructions apply to a Fedora VM running inside UTM on macOS.

---

## 1. Update System Packages

Before configuring anything, ensure the system packages are up to date:

```bash
sudo dnf update -y
```

## 2. Install the OpenSSH Server

The SSH daemon (sshd) is required to allow remote connections.

```bash
sudo dnf install -y openssh-server
```

## 3. Enable and Start the SSH Service

Ensure SSH starts automatically on boot and is running now:

```bach
sudo systemctl enable --now sshd
```

## 4. Allow SSH Through the Firewall

Fedora uses firewalld.
Open port 22 permanently:

```bash
sudo firewall-cmd --add-service=ssh --permanent
sudo firewall-cmd --reload
```

Check the rules:

```bash
sudo firewall-cmd --list-all
```

##5. Verify That SSH is Listening

Use ss to confirm that the SSH daemon is listening on port 22:

```bash
sudo ss -tulnp | grep 22
```

Expected output:

LISTEN 0 128 0.0.0.0:22 0.0.0.0:* users:(("sshd",pid=XYZ,fd=3))

##6. Check the IP Address of the VM

To connect from an external device (e.g., iPhone), you need the VM’s IP address:

```bash
ip a
```

Look for the address under eth0 or enp0s*, depending on your network adapter.

## 7. Test the Connection Locally

From macOS Terminal, test SSH:

```bash
ssh username@<your-fedora-ip>
```

If you can log in — the installation is successful.

## 8. Connect From iPhone (Optional)

If connecting from iTerminal:
	1.	Open iTerminal
	2.	Choose SSH
	3.	Add new connection:
	•	Host: your Fedora IP
	•	Port: 22
	•	Username: Fedora login
	•	Password: Fedora password
	4.	Save and connect

## Summary

After completing this installation process, the Fedora VM is ready for remote access and further configuration.
This setup lays the foundation for Linux administration, DevOps practice, service management, and troubleshooting.