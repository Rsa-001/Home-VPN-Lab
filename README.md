# 🏠 Home VPN Lab with OpenVPN

This project demonstrates how to create a self-hosted VPN using **OpenVPN** on a **Linux virtual machine** running inside **VMware Workstation Pro** (using NAT - `vmnet9`). The goal is to provide secure remote access to your home network, as if you were physically connected to it.

In this guide, I use a Linux virtual machine hosted on VMware Workstation Pro (NAT mode via `vmnet9`) as the OpenVPN server. This setup makes it easy to test, snapshot, and reset the environment. The steps are identical if you run the server on a physical host or a different VM/hypervisor; you only need to adapt the port forwarding/NAT section to match your environment.

Write up --> https://rsas-book.gitbook.io/rsas-book/projects/home-vpn-lab

---

## 📌 Features

* Fully functional OpenVPN server
* Clients can connect securely from anywhere in the world
* NAT + IP forwarding setup for full internet access
* Embedded certificates in `.ovpn` for easier distribution
* Works in any hypervisor or physical host (adjust NAT/forwarding accordingly)

---

## 📁 Project Structure

```
/openvpn-home-lab
├── server.conf          # OpenVPN server configuration
├── client.ovpn          # Example client configuration with embedded certs
├── .keypass             # Encrypted key passphrase (optional)
├── easy-rsa/            # Easy-RSA structure for key/cert generation
└── README.md
```

---

## 🛠 Requirements

* VMware Workstation Pro (or any hypervisor)
* Linux-based VM (Debian/Ubuntu recommended)
* `openvpn`, `easy-rsa`
* Basic networking knowledge

---

## ⚙️ Key Configuration Steps

1. Enable IPv4 forwarding:

   ```bash
   sudo sysctl -w net.ipv4.ip_forward=1
   ```

2. Set up NAT using VMware’s `vmnet9` or your own interface (adapt forwarding rules).

3. Configure OpenVPN server (`server.conf`) and embed required keys.

4. Export a `.ovpn` file for your clients with:

   * `<ca>...</ca>`
   * `<cert>...</cert>`
   * `<key>...</key>`
   * `<tls-auth>...</tls-auth>`

5. Use port forwarding on VMware or your router to expose UDP 1194.

---

## 🧪 Why Use a VM?

Using a VM simplifies testing and allows rollback via snapshots. While a virtual machine is used in this lab, OpenVPN can run on any Linux system — including Raspberry Pi, dedicated server, or cloud instance — as long as the required networking setup (port forwarding, NAT, IP forwarding) is in place.

---

## 🔐 Security Notes

* Always encrypt private keys (`.key`) with a passphrase
* Avoid sharing `.ovpn` files without protection
* Use `auth-nocache` to prevent password retention in memory

---

## 📚 License

This project is for educational use only. Use responsibly.

Created for learning and secure home lab access.

