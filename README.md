# GNS3 Lab Requirements and Setup Guide

This repository contains various Cisco network configuration labs, mainly focusing on dynamic routing protocols like OSPF, EIGRP, and BGP.

To run these labs, you need to install **GNS3** along with its required **GNS3 VM**. Below are the instructions and recommendations to get started.

---

## 🚀 What is GNS3?

**GNS3 (Graphical Network Simulator 3)** is a network emulation tool used by network engineers to simulate complex networks without requiring physical hardware. It supports real Cisco IOS images and other virtual appliances like Linux, Windows, and security tools.

GNS3 is especially useful for CCNA, CCNP, and CCIE lab practice.

---

## 🖥️ Requirements

### 1. GNS3 Software (GUI)

- Acts as the frontend interface where you design topologies.
- Available for Windows, macOS, and Linux.

Download from: [https://www.gns3.com/software/download](https://www.gns3.com/software/download)

### 2. GNS3 VM (Virtual Machine)

- Required to run Cisco IOS, IOU, and other advanced appliances using Dynamips, QEMU, and Docker.
- Runs on VMware Workstation, VMware Fusion, or VirtualBox.
- Communicates with the GNS3 GUI to handle processing-heavy tasks.

Download from: [https://www.gns3.com/software/download-vm](https://www.gns3.com/software/download-vm)

---

## 🔧 Installation Summary

1. **Install GNS3 GUI** on your local machine.
2. **Import the GNS3 VM** into your virtualization software (recommended: VMware Workstation/Fusion).
3. Configure GNS3 to connect to the VM (under Preferences > GNS3 VM).
4. Add necessary images:
   - Cisco IOS images (e.g., `c7200`, `c3725`, or `IOSv`)
   - Cisco IOU/IOL (if using Linux or for more scalable labs)
   - Docker containers for network tools (optional)

---

## 📦 Suggested Images

| Type      | Name / Version                         | Notes                            |
|-----------|----------------------------------------|----------------------------------|
| IOS       | `c7200-adventerprisek9-mz.152-4.M7.bin` | Stable for routing labs          |
| IOU/IOL   | `i86bi-linux-l2` and `i86bi-linux-l3`   | Scalable, requires IOU license   |
| Others    | `VPCS`, `TinyCore`, `Alpine Linux`      | Lightweight host emulation       |

---

## 📁 Folder Structure

```
labs/
├── ospf-path-filtering/
│   ├── README.md
│   └── project.gns3
├── eigrp-basic/
│   ├── README.md
│   └── topology.gns3
└── ...
```

---

## 🧠 Tips

- Use **"Save As Project"** in GNS3 to export/share labs easily.
- Enable **"Always use GNS3 VM"** for consistent performance.
- Use `VPCS` or small Linux VMs for end-host emulation.

---

## 📞 Need Help?

Visit the [GNS3 Community Forums](https://community.gns3.com/) or check their [official documentation](https://docs.gns3.com/).

---

Happy Labbing! 🧪🌐
