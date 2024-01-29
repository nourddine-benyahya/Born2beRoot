
# Virtualization 🚀

Virtualization is the process of creating a software-based (virtual) version of something using hypervisor software. This can include virtualizing compute, storage, networking, servers, or applications.


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
- **VM** from Oracle
- **Open source KVM**

#### Type 2 Hypervisor (Hosted Hypervisor)
A Type 2 hypervisor is a virtualization technology that runs on a conventional operating system just like any other software application. It is often used for desktop virtualization and testing purposes, allowing users to run multiple virtual machines on their personal computers without dedicated hardware support
Examples of Type 2 hypervisors include:
- **VMware**
- **Oracle VirtualBox**
- **Client Hyper-V**


## Hardware Requirements 💾

To enable virtualization, your hardware should meet the following requirements:
- CPU must support hardware-assisted virtualization (HAV)
- Enable virtualization technology in EFI BIOS
- Strong processor and memory
- Adequate hard drive space

---

# VirtualBox 🚀

## What is a VirtualBox

VirtualBox is open-source software for virtualizing the x86 computing architecture. It acts as a hypervisor type 2, creating a VM  where the user can run another OS .

The operating system where VirtualBox runs is called the "host" OS. The operating system running in the VM is called the "guest" OS. VirtualBox supports Windows, Linux, or macOS as its host OS.

## UTM vs VirtualBox: Which is Better for Virtual Machines?

As a Mac user you have two superb choices available for running virtual machines, both are open source and both are entirely free.

- **VirtualBox** is a well known solution for creating virtual machines offered by heavyweight computer technology company Oracle. It was originally released in 2007 and is available for macOS, Windows and Linux hosts.

- **UTM** (Universal Turing Machine) is actually a frontend GUI for the all-powerful open source emulation platform QEMU, offering a beautiful interface native to Apple products. It is available for both macOS and iOS devices.


# Operating System 🚀

Operating System basically its manages all the resources of the computer we can say acts as an interface between the software and different parts of the computer or the computer hardware.

## What is a distribution

A Linux distribution, is an operating system compiled from components developed by various open source projects and programmers. Each distribution includes the Linux kernel (the foundation of the operating system), the GNU shell utilities (the terminal interface and commands), the X server (for a graphical desktop), the desktop environment, a package management system, an installer and other services.


### Debian

Debian also known as Debian GNU/Linux, is a Linux distribution composed of free and open-source software, developed by the community-supported Debian Project. The Debian Stable branch is the most popular edition for personal computers and servers. Debian is also the basis for many other distributions, most notably Ubuntu, Pardus, Linux Mint.

Debian is one of the oldest operating systems based on the Linux kernel

### Rocky Linux

Rocky Linux was founded by one of the co-founders of CentOS, after Red Hat discontinued CentOS.

Rocky represents what CentOS used to be when it was established - a downstream distribution of Red Hat Enterprise Linux, stable, completely compatible with RHEL, and it is ideal for servers. Kurtzer took the RHEL open-source code and, using his background in high-performance scientific computing, created Rocky Linux as a CentOS doppelganger - but completely free.

### Differences between Rocky Linux and Debian

| **Aspect**              | **Rocky Linux**                                 | **Debian**                                      |
|-------------------------|-------------------------------------------------|-------------------------------------------------|
| **Origin**              | Fork of RHEL (Red Hat Enterprise Linux)        | Independent, community-driven                    |
| **Stability**           | Stable, focused on enterprise environments     | Stable, well-established, widely used           |
| **Release Cycle**       | Regular releases based on RHEL                  | Regular releases with well-defined schedules    |
| **Package Management**  | **YUM/DNF:** Package manager for RPM packages  | **APT:** Advanced Package Tool for DEB packages |
| **Init System**         | **Systemd:** Modern init and system management  | **SysVinit:** Traditional UNIX init system       |
| **Default Desktop**     | Minimal installation, no default desktop        | Minimal installation, various desktop options    |
| **Security**            | SELinux available, enabled by default            | AppArmor available; security emphasis            |
| **Community Support**   | Growing community support due to CentOS shift   | Long-standing, large, diverse community          |
| **Documentation**       | Documentation available, improving over time    | Extensive and mature documentation               |
| **Use Cases**           | Server deployments, enterprise environments     | General-purpose, server, and desktop usage       |
| **Commercial Support**  | Community-driven, with potential commercial use | Limited commercial support available             |
| **Licensing**           | Open Source (GNU GPL and other licenses)        | Free Software (Debian Free Software Guidelines)  |


##TCP VS UDP
  https://youtu.be/uwoD5YsGACg?si=hjAu8NIE-CByzmjJ

#script

The architecture of your operating system and its kernel version.
```
uname -a | awk 'printf "#Architecture %s/n", $0'
```
• The number of physical processors.
```
lscpu | grep '^CPU(s) :' | awk '{printf "#CPU physical : %d\n", $2}'
```
• The number of virtual processors.
```
nproc | awk '{printf "#vCPU : %d\n", $0}'
```
• The current available RAM on your server and its utilization rate as a percentage.
```
free -m | grep Mem: | awk '{printf "#Memory Usage: %d/%dMB (%.1f%%)\n", $3, $2, ($3/$2)*100}'
```
• The current available memory on your server and its utilization rate as a percentage.
```
df -m --total | grep 'total' | awk '{printf "#Disk Usage: %d/%dGb (%.1f%%)\n", $3, $4/1024, ($3/$4)*100}'
```
• The current utilization rate of your processors as a percentage.
```
mpstat | tail -n 1 | awk '{printf "#CPU load: %.1f%%\n", 100 - $13}'
```
• Whether LVM is active or not.
```
lsblk | grep ' lvm ' | tail -n -1 | awk '{printf "#LVM use :"; if ($0) print "yes"; else print "no"}'
```
• The number of active connections.
```
netstat -at | grep ESTABLISHED | wc -l | awk '{print "#Connections TCP : " $1 " ESTABLISHED"}'
```
• The number of users using the server.
```
who | awk '{print $1}' | sort -u | wc -l
```
• The IPv4 address of your server and its MAC (Media Access Control) address.
```
hostname -i
ip link show | grep link/ether | awk '{print $2}'
```
• The number of commands executed with the sudo program.
```
cat /var/log/sudo/sudo.log | grep 'COMMAND' | wc -l | awk '{print "#Sudo : " ($1) " cmd"}'
```
# Script using wall
```
#!/bin/bash

wall <<EOF
#Architecture 	 : $(uname -a | sed 's/ PREEMPT_DYNAMIC//')
#CPU physical 	 : $(lscpu | grep '^CPU(s):' | awk '{print $2}')
#vCPU		 : $(nproc)
#Memory Usage	 : $(free -m | grep Mem: | awk '{printf "%d/%dMB (%.1f%%)\n", $3, $2, ($3/$2)*100}')
#Disk Usage	 : $(df -m --total | grep 'total' | awk '{printf "%d/%dGb (%.1f%%)\n", $3, $4/1024, ($3/$4)*100}')
#CPU load 	 : $(mpstat | tail -n 1 | awk '{printf "%.1f%%\n", 100 - $13}')
#LVM use 	 : $(lsblk | grep ' lvm ' | tail -n -1 | awk '{printf "%s\n", ($0 ? "yes" : "no")}')
#Connections TCP : $(netstat -at | grep ESTABLISHED | wc -l) ESTABLISHED
#User log	 : $(who | awk '{print $1}' | sort -u | wc -l)
#Network	 : IP $(hostname -I) ($(ip link show | grep link/ether | awk '{print $2}'))
#Sudo		 : $(cat /var/log/sudo/sudo.log | grep 'COMMAND' | wc -l) cmd
EOF
```
