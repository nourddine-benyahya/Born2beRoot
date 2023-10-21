# Virtualization 🚀

Virtualization is the process of creating a software-based (virtual) version of something using hypervisor software. This can include virtualizing compute, storage, networking, servers, or applications.

---

## Host and Hypervisor 💻

### Hypervisor Definition:
A hypervisor is a software, firmware, or hardware component that creates and manages virtual machines (VMs) on a physical computer. It allows multiple operating systems to run concurrently on a single host

### Types of Hypervisors:

![Types of Hypervisors](./images/server_virt-hypervisor.jpg)

#### Type 1 Hypervisor (Bare Metal Hypervisor)
A Type 1 hypervisor is a virtualization technology that runs directly on the hardware of a host system without the need for an underlying operating system. It provides high performance and is typically used in enterprise environments for server virtualization
Examples of Type 1 hypervisors include:
- **XenServer** by Citrix
- **ESXi** by VMware
- **Hyper-V** from Microsoft
- **VirtualBox** from Oracle
- **Open source KVM**

#### Type 2 Hypervisor (Hosted Hypervisor)
A Type 2 hypervisor is a virtualization technology that runs on a conventional operating system just like any other software application. It is often used for desktop virtualization and testing purposes, allowing users to run multiple virtual machines on their personal computers without dedicated hardware support
Examples of Type 2 hypervisors include:
- **VMware**
- **Oracle VirtualBox**
- **Client Hyper-V**

---

## Hardware Requirements 💾

To enable virtualization, your hardware should meet the following requirements:
- CPU must support hardware-assisted virtualization (HAV)
- Enable virtualization technology in EFI BIOS
- Strong processor and memory
- Adequate hard drive space

