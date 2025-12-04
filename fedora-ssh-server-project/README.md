# Remote Access to Fedora VM (UTM + SSH)


![Fedora](https://img.shields.io/badge/Fedora-OS-blue)
![SSH](https://img.shields.io/badge/SSH-Enabled-success)
![UTM](https://img.shields.io/badge/UTM-Virtualization-orange)
![Docs](https://img.shields.io/badge/Docs-Complete-brightgreen)

This project provides a minimal and secure setup for remote SSH access to a Fedora Linux virtual machine running inside UTM on macOS.  
The goal is to practice Linux, system administration, and remote connectivity using an iPhone as an SSH client.

---

## 📦 Features

- Fedora VM running inside UTM  
- SSH access from iPhone (iTerminal)  
- FirewallD and SELinux configured  
- systemd-managed sshd service  
- Clean documentation and modular project structure

---

## 📚 Documentation

The project contains structured documentation located in the `docs/` directory:

### 🔧 Installation  
Step-by-step setup guide for UTM, Fedora, SSH, networking, and firewall:

👉 **[Installation Guide](./docs/installation.md)**

### 🧱 Architecture  
System architecture with components description and Mermaid diagram:

👉 **[Architecture](./docs/architecture.md)**

### ❗ Troubleshooting  
Common problems and fixes (SSH issues, networking, UTM settings):

👉 **[Troubleshooting](./docs/troubleshooting.md)**

---

## 📁 Project Structure

```
/project-root
│
├── README.md
└── docs/
    ├── installation.md
    ├── architecture.md
    └── troubleshooting.md
```

---

## 📝 Notes

- The project is designed for real remote SSH practice using mobile devices.  
- Works offline inside a NAT-based virtual environment.  
- Supports future expansion (SSH keys, VPN, automation scripts, hardening).

---

## 📄 License

This project is provided for learning and personal use.