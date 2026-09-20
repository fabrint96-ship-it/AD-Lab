# AD-Lab — Setup

## 1. Purpose

This document records the reproducible setup process for Active Directory Lab / AD-Lab.

It describes how the laboratory foundation is prepared and will be expanded as implementation progresses.

The document does not replace block-specific evidence. Evidence records what was actually executed and validated, while this document describes the reproducible setup process.

---

## 2. Host Requirements

Current validated host baseline:

```
Operating System: Windows 11
CPU: Intel Core i5-11400H
Physical cores: 6
Logical processors: 12
RAM: approximately 16 GB
```

Hardware virtualization must be available.

The current host uses Hyper-V and Virtualization-Based Security.

---

## 3. Virtualization Platform

AD-Lab uses:

```
Oracle VirtualBox 7.2.18
```

Validated version:

```
7.2.18r175117
```

No VirtualBox Extension Pack is required by the current laboratory baseline.

---

## 4. Operational Storage

Create:

```
D:\Labs\AD-Lab\
```

Required structure:

```
D:\Labs\AD-Lab\
├── VirtualMachines\
│   ├── DC01\
│   ├── SRV01\
│   ├── PC01\
│   └── PC02\
├── ISO\
├── Backups\
└── Exports\
```

Configure VirtualBox default machine storage as:

```
D:\Labs\AD-Lab\VirtualMachines
```

Example:

```
VBoxManage setproperty machinefolder "D:\Labs\AD-Lab\VirtualMachines"
```

Validate:

```
VBoxManage list systemproperties
```

---

## 5. Virtual Network

Create a dedicated VirtualBox NAT Network:

```
Name: AD-LAB-NET
Network: 10.10.10.0/24
Gateway: 10.10.10.1
VirtualBox DHCP: Disabled
```

Creation command:

```
VBoxManage natnetwork add `
    --netname "AD-LAB-NET" `
    --network "10.10.10.0/24" `
    --enable `
    --dhcp off
```

Validate:

```
VBoxManage list natnets
```

Expected core state:

```
Name:         AD-LAB-NET
Network:      10.10.10.0/24
Gateway:      10.10.10.1
DHCP Server:  No
```

VirtualBox DHCP must remain disabled for this network because DHCP will later be provided by Windows Server.

---

## 6. Virtual Machines

Create the following machines.

### DC01

```
Guest OS type: Windows2025_64
vCPU: 2
RAM: 3072 MB
Disk: 61440 MB dynamic VDI
Network: AD-LAB-NET
```

### SRV01

```
Guest OS type: Windows2025_64
vCPU: 2
RAM: 3072 MB
Disk: 81920 MB dynamic VDI
Network: AD-LAB-NET
```

### PC01

```
Guest OS type: Windows11_64
vCPU: 2
RAM: 3072 MB
Disk: 65536 MB dynamic VDI
Network: AD-LAB-NET
```

### PC02

```
Guest OS type: Windows11_64
vCPU: 2
RAM: 3072 MB
Disk: 65536 MB dynamic VDI
Network: AD-LAB-NET
```

Each VM uses a SATA controller and dynamically allocated VDI.

Each VM also has an empty virtual optical drive prepared for installation media.

---

## 7. VM Validation

List registered machines:

```
VBoxManage list vms
```

List running machines:

```
VBoxManage list runningvms
```

Inspect an individual VM:

```
VBoxManage showvminfo "<VM>" --machinereadable
```

Inspect a virtual disk:

```
VBoxManage showmediuminfo "<VDI path>"
```

Verify at minimum:

* Correct VM name.
* Correct guest OS type.
* Correct RAM.
* Correct vCPU count.
* NAT Network adapter.
* `AD-LAB-NET` assignment.
* Correct VDI capacity.
* Correct disk attachment.

---

## 8. Resource Management

The host has approximately 16 GB RAM.

Each initial VM is configured with:

```
3072 MB
```

All four machines are not required to run simultaneously.

A normal multi-machine scenario is expected to use:

```
DC01 + SRV01 + PC01
```

which represents approximately 9 GB of configured guest RAM.

Check available host memory before starting several VMs simultaneously.

---

## 9. Planned Network Configuration

The guest operating systems will later use:

```
Network: 10.10.10.0/24
Gateway: 10.10.10.1
```

Planned infrastructure:

```
DC01   10.10.10.10
SRV01  10.10.10.20
```

Planned DNS:

```
10.10.10.10
```

Planned DHCP pool:

```
10.10.10.100 - 10.10.10.199
```

PC01 and PC02 will eventually receive their network configuration from the Windows Server DHCP service.

Guest OS network configuration is intentionally not part of the Virtualization Foundation.

---

## 10. Snapshot Plan

Create strategic snapshots as implementation reaches the corresponding state:

```
S00-Clean-Install
S01-Network-Configured
S02-Before-ADDS
S03-ADDS-Operational
S04-Before-GPO
```

Do not treat snapshots as backups.

---

## 11. Repository

Local Git repository:

```
D:\Proyectos\AD-Lab
```

Operational infrastructure:

```
D:\Labs\AD-Lab
```

These locations serve different purposes and must remain separated.

The repository stores:

* Documentation.
* Scripts.
* Configuration exports.
* Evidence.
* Diagrams.
* Troubleshooting records.

It must not store:

* VDI/VHD/VMDK files.
* ISO images.
* VM exports.
* Backups.
* Passwords.
* Tokens.
* Private keys.
* Other secrets.

---

## 12. Current Setup State

At the end of the Virtualization Foundation implementation:

* VirtualBox 7.2.18 is installed.
* Hardware virtualization is available.
* `D:\Labs\AD-Lab` exists.
* VirtualBox uses the approved VM folder.
* `AD-LAB-NET` exists.
* VirtualBox DHCP is disabled on the lab network.
* DC01 exists.
* SRV01 exists.
* PC01 exists.
* PC02 exists.
* All four machines are registered.
* All four machines use `AD-LAB-NET`.
* No guest operating system has yet been installed.
