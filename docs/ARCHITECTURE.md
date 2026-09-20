# AD-Lab — Architecture

## 1. Purpose

This document defines the architectural baseline of Active Directory Lab / AD-Lab.

The laboratory represents a small/medium business Microsoft infrastructure designed for practical systems administration training, technical validation and professional portfolio evidence.

The architecture is intended to evolve progressively without requiring redesign of the initial foundation.

---

## 2. Organization

**Organization:** ContosoLab

**Active Directory DNS domain:**

```
ad.contosolab.test
```

**NetBIOS domain:**

```
CONTOSOLAB
```

Initial departments:

* Direction
* IT
* Administration
* HR
* Finance
* Sales
* Support

---

## 3. Initial Topology

```
INTERNET
   |
VirtualBox NAT
Gateway: 10.10.10.1
   |
AD-LAB-NET
10.10.10.0/24
   |
   +---- DC01
   |
   +---- SRV01
   |
   +---- PC01
   |
   +---- PC02
```

All initial virtual machines share the dedicated `AD-LAB-NET` VirtualBox NAT Network.

---

## 4. Network Architecture

### Network

```
10.10.10.0/24
```

### Default Gateway

```
10.10.10.1
```

### Planned Infrastructure Addresses

| Device  | Address     | Allocation     |
| ------- | ----------- | -------------- |
| Gateway | 10.10.10.1  | VirtualBox NAT |
| DC01    | 10.10.10.10 | Static         |
| SRV01   | 10.10.10.20 | Static         |
| PC01    | DHCP        | Dynamic        |
| PC02    | DHCP        | Dynamic        |

### DNS

Planned authoritative DNS server for domain clients:

```
10.10.10.10
```

Domain clients must use the Active Directory DNS infrastructure rather than external DNS servers directly.

### DHCP

Planned DHCP client pool:

```
10.10.10.100 - 10.10.10.199
```

Addresses outside the dynamic pool are reserved for infrastructure, exclusions, reservations or future expansion as appropriate.

VirtualBox DHCP is disabled on `AD-LAB-NET`.

The Windows Server DHCP role planned for DC01 will become the authoritative DHCP service for the laboratory.

---

## 5. Virtualization Architecture

### Platform

```
Oracle VirtualBox 7.2.18
```

### Host

Validated B1 host baseline:

```
Operating System: Windows 11
Version: 10.0.26200.9457
CPU: Intel Core i5-11400H
Physical cores: 6
Logical processors: 12
RAM: approximately 16 GB
```

Hardware virtualization and nested paging are available.

Hyper-V and Virtualization-Based Security remain enabled on the host.

### VirtualBox Machine Folder

```
D:\Labs\AD-Lab\VirtualMachines
```

### Virtual Network

```
AD-LAB-NET
10.10.10.0/24
```

VirtualBox NAT gateway:

```
10.10.10.1
```

VirtualBox DHCP:

```
Disabled
```

---

## 6. Virtual Machine Architecture

### DC01

```
Operating System: Windows Server 2025 Desktop Experience
vCPU: 2
RAM: 3072 MB
Disk: 60 GiB dynamic VDI
Network: AD-LAB-NET
```

Planned responsibilities:

* Domain Controller.
* Active Directory Domain Services.
* Active Directory-integrated DNS.
* DHCP.

### SRV01

```
Operating System: Windows Server 2025 Desktop Experience
vCPU: 2
RAM: 3072 MB
Disk: 80 GiB dynamic VDI
Network: AD-LAB-NET
```

Planned responsibilities:

* Domain member server.
* File services.
* Departmental shares.
* Auxiliary infrastructure services where justified.

### PC01

```
Operating System: Windows 11
vCPU: 2
RAM: 3072 MB
Disk: 64 GiB dynamic VDI
Network: AD-LAB-NET
```

Planned responsibility:

* Domain workstation.

### PC02

```
Operating System: Windows 11
vCPU: 2
RAM: 3072 MB
Disk: 64 GiB dynamic VDI
Network: AD-LAB-NET
```

Planned responsibility:

* Domain workstation.

---

## 7. Active Directory Logical Architecture

The initial architecture uses:

```
1 Forest
1 Domain
```

Forest/domain:

```
ad.contosolab.test
```

NetBIOS:

```
CONTOSOLAB
```

DC01 will become the initial Domain Controller.

### OU Structure

Planned structure:

```
ContosoLab
|
+-- Users
|   +-- Direction
|   +-- IT
|   +-- Administration
|   +-- HR
|   +-- Finance
|   +-- Sales
|   +-- Support
|
+-- Computers
|   +-- Workstations
|   +-- Laptops
|
+-- Servers
|
+-- Service Accounts
|
+-- Disabled Objects
```

The default `Domain Controllers` OU remains responsible for Domain Controller computer objects.

A separate Groups OU is not part of the initial baseline and will only be introduced if later implementation requirements justify it.

---

## 8. Identity Naming

Standard user accounts:

```
firstname.lastname
```

Example:

```
daniel.ruiz
```

Administrative accounts:

```
adm.firstname.lastname
```

Example:

```
adm.daniel.ruiz
```

Service accounts:

```
svc.<service>
```

Computer naming:

```
DC##       Domain Controllers
SRV##      Member Servers
FILE##     Dedicated File Servers
PC##       Windows Clients
```

---

## 9. Authorization Model

AD-Lab will use security groups instead of assigning resource permissions directly to individual users whenever practical.

The preferred authorization model is:

```
Accounts
   ↓
Global Groups
   ↓
Domain Local Groups
   ↓
Permissions
```

AGDLP will be applied where appropriate.

Example:

```
User
  ↓
GG_Finance
  ↓
DL_Finance_RW
  ↓
NTFS / Share Permission
```

Direct user-to-resource permissions should be avoided unless explicitly justified and documented.

---

## 10. Storage Architecture

Operational laboratory infrastructure:

```
D:\Labs\AD-Lab\
```

Structure:

```
AD-Lab
|
+-- VirtualMachines
|   +-- DC01
|   +-- SRV01
|   +-- PC01
|   +-- PC02
|
+-- ISO
+-- Backups
+-- Exports
```

Git repository:

```
D:\Proyectos\AD-Lab\
```

Operational infrastructure and Git documentation are deliberately separated.

VM disks, installation media, backups and exports must not be committed to Git.

---

## 11. Snapshot Strategy

Strategic snapshot names:

```
S00-Clean-Install
S01-Network-Configured
S02-Before-ADDS
S03-ADDS-Operational
S04-Before-GPO
```

Snapshots are operational recovery points for laboratory work.

A snapshot is not considered a backup.

---

## 12. Future Expansion

The architecture must support future additions without redesigning the foundation.

Potential additions include:

* FILE01.
* Backup Server.
* Monitoring Server.
* Additional Domain Controller.
* Linux Server.
* VPN.
* GLPI.
* Docker workloads.
* Additional Windows clients.
* Additional infrastructure services.

Any expansion must preserve documented naming, addressing, security and evidence conventions.

---

## 13. Architectural Principles

The laboratory follows these principles:

* Evidence before assumption.
* Reproducibility.
* Least privilege.
* Separation of administrative and standard identities.
* Group-based authorization.
* DNS correctness as a core Active Directory dependency.
* Controlled infrastructure changes.
* Validation after implementation.
* Documentation before block closure.
* No secrets in Git.
* Operational infrastructure separated from documentation and source control.
