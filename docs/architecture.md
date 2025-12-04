# System Architecture — Remote Access Fedora

## 1. Overview
This project enables secure remote access to a Fedora Linux virtual machine running inside UTM on macOS.  
The VM is configured to accept SSH connections from an external client (iPhone), providing a minimal and reliable setup for remote Linux practice and administration.

The architecture consists of a client layer, a virtualized network, the Fedora VM, system services, and a dedicated security layer.

---

## 2. Components

### **Client Layer**
- **Device:** iPhone  
- **Application:** iTerminal (SSH client)  
- Connects to the Fedora VM over port **22/tcp**

### **Network Layer**
- UTM Virtual Network (NAT mode)  
- Provides internal connectivity between iPhone ↔ VM  
- Fedora typically receives an internal NAT IP (e.g., 192.168.x.x)

### **Fedora VM Layer**
- Fedora Linux minimal installation  
- OpenSSH Server (sshd) installed and enabled  
- Local user with password authentication

### **System Services Layer**
- **systemd** manages system processes  
- Controls `sshd.service`  
- Ensures automatic SSH server startup on boot

### **Security Layer**
- **SSH Authentication:** password-based (or key-based if added)  
- **FirewallD:** port `22/tcp` explicitly allowed  
- **SELinux:** provides mandatory access control (enforcing or permissive mode)

### **Logging & Monitoring**
- `journalctl -u sshd` — view SSH logs  
- Useful for debugging login attempts and service state

---

## 3. Connection Flow

1. User opens iTerminal on iPhone  
2. SSH request sent to Fedora VM via NAT network  
3. NAT transfers traffic to VM internal IP  
4. Fedora receives SSH request → `sshd` handles authentication  
5. systemd ensures sshd stays active  
6. Successful login opens a remote shell session

---

## 4. Architecture Diagram

```mermaid
flowchart TD

    A[iPhone<br>SSH Client (iTerminal)]
    B[UTM Virtual Network<br>(NAT)]
    C[Fedora VM]
    D[System Services<br>systemd → sshd.service]
    E[Security Layer<br>- SSH Auth<br>- FirewallD 22/tcp<br>- SELinux]
    F[Logging<br>journalctl -u sshd]

    A -- SSH over 22/tcp --> B
    B --> C
    C --> D
    C --> E
    C --> F
```

---

## 5. Requirements

- UTM installed on macOS  
- Fedora VM with OpenSSH server  
- SSH client on iPhone (iTerminal)  
- NAT mode enabled for UTM  
- FirewallD configured to allow port 22  
- SELinux mode not blocking sshd (permissive/enforcing allowed)

---

## 6. Notes

- For security, consider switching from password authentication to SSH keys later.  
- Ensure the VM does not enter sleep mode during remote sessions.  