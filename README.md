# Active Directory Lab / AD-Lab

Professional Microsoft Active Directory and Windows Server laboratory designed as a practical systems administration portfolio project.

## Project Status

**Current phase:** Implementation
**Current block:** B1 — Virtualization Foundation
**B0 — Planning & Design:** Completed
**B1 — Virtualization Foundation:** Documentation and closure in progress

## Objective

Build a reproducible small/medium business Windows infrastructure laboratory demonstrating practical administration skills in:

* Windows Server.
* Active Directory Domain Services.
* DNS.
* DHCP.
* Group Policy.
* Organizational Units.
* Users and security groups.
* Windows domain clients.
* NTFS permissions.
* File sharing.
* Security hardening.
* PowerShell automation.
* Monitoring and auditing.
* Troubleshooting.
* Backup and recovery.
* Technical documentation.
* Git and GitHub.

The project is intended to be reproducible, technically validated and suitable for demonstration in a technical interview or professional portfolio.

## Organization

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

## Initial Infrastructure

| Device | Operating System                       | Initial Role                                       |
| ------ | -------------------------------------- | -------------------------------------------------- |
| DC01   | Windows Server 2025 Desktop Experience | Domain Controller, DNS, DHCP                       |
| SRV01  | Windows Server 2025 Desktop Experience | Member Server / future file and auxiliary services |
| PC01   | Windows 11                             | Domain workstation                                 |
| PC02   | Windows 11                             | Domain workstation                                 |

## Network

**Laboratory network:**

```
10.10.10.0/24
```

**Gateway:**

```
10.10.10.1
```

**Planned infrastructure addresses:**

```
DC01    10.10.10.10
SRV01   10.10.10.20
```

**Planned DHCP range:**

```
10.10.10.100 - 10.10.10.199
```

**Planned DNS server:**

```
10.10.10.10
```

## Virtualization

Virtualization platform:

```
Oracle VirtualBox 7.2.18
```

Dedicated VirtualBox network:

```
AD-LAB-NET
```

Virtual network:

```
10.10.10.0/24
```

VirtualBox NAT gateway:

```
10.10.10.1
```

VirtualBox DHCP is disabled on `AD-LAB-NET`.

The future Windows Server DHCP service on DC01 will provide addressing to domain clients.

## Virtual Machines

| VM    | Guest OS                | vCPU |     RAM |       Virtual Disk |
| ----- | ----------------------- | ---: | ------: | -----------------: |
| DC01  | Windows Server 2025 x64 |    2 | 3072 MB | 60 GiB dynamic VDI |
| SRV01 | Windows Server 2025 x64 |    2 | 3072 MB | 80 GiB dynamic VDI |
| PC01  | Windows 11 x64          |    2 | 3072 MB | 64 GiB dynamic VDI |
| PC02  | Windows 11 x64          |    2 | 3072 MB | 64 GiB dynamic VDI |

All four machines use:

```
AD-LAB-NET
```

## Storage Separation

Operational laboratory infrastructure is stored outside Git:

```
D:\Labs\AD-Lab\
```

This location contains:

* Virtual machines.
* Installation media.
* Backups.
* Virtual machine exports.

The Git repository is stored separately:

```
D:\Proyectos\AD-Lab\
```

Virtual disks, ISOs, backups, exports, credentials and secrets must never be committed to the repository.

## Repository Structure

```
AD-Lab/
├── configs/
│   ├── active-directory/
│   ├── dhcp/
│   ├── dns/
│   ├── file-server/
│   └── gpo/
├── diagrams/
│   ├── active-directory/
│   ├── network/
│   └── topology/
├── docs/
│   └── blocks/
├── evidence/
├── scripts/
│   └── powershell/
├── .gitignore
└── README.md
```

The repository will grow progressively as each laboratory block is implemented.

## Implementation Roadmap

| Block | Description                      |
| ----- | -------------------------------- |
| B0    | Planning & Design                |
| B1    | Virtualization Foundation        |
| B2    | Network Foundation               |
| B3    | Windows Server Foundation        |
| B4    | Active Directory Deployment      |
| B5    | DNS                              |
| B6    | DHCP                             |
| B7    | OU, Users & Groups               |
| B8    | Windows Clients                  |
| B9    | Group Policy                     |
| B10   | File Server & Permissions        |
| B11   | PowerShell Automation            |
| B12   | Security Hardening               |
| B13   | Monitoring & Auditing            |
| B14   | Troubleshooting Scenarios        |
| B15   | Backup & Recovery                |
| B16   | Final Validation                 |
| B17   | GitHub Documentation & Portfolio |

## Engineering Workflow

Each implementation block follows:

```
PLAN
  ↓
PREPARE
  ↓
IMPLEMENT
  ↓
VERIFY
  ↓
CAPTURE EVIDENCE
  ↓
DOCUMENT
  ↓
REVIEW
  ↓
RECORD
  ↓
CLOSE
```

A configuration is not considered complete merely because it appears to work in a graphical interface.

Validation should preferentially use:

* Commands.
* Configuration queries.
* Logs.
* Functional tests.
* Diagnostic tools.

## Evidence

Technical evidence is stored under:

```
evidence/
```

Textual evidence uses Markdown.

Standard naming convention:

```
<DEVICE>-<BLOCK>-<DESCRIPTION>.md
```

Evidence should record:

* Objective.
* Commands.
* Relevant original output.
* PASS/FAIL result.
* Notes.

## Security

This repository must never contain:

* Real passwords.
* API tokens.
* Private keys.
* Credentials.
* Sensitive personal information.
* VM disks.
* ISO images.
* Large unnecessary binaries.

## Current Progress

### B0 — Planning & Design

**Status:** COMPLETED

The initial architecture, naming conventions, addressing plan, Active Directory logical design, repository design and implementation roadmap have been defined.

### B1 — Virtualization Foundation

**Status:** DOCUMENTING

Completed technical work includes:

* VirtualBox baseline validation.
* Upgrade to VirtualBox 7.2.18.
* Hardware virtualization validation.
* Hyper-V/VBS compatibility validation.
* Host storage preparation.
* VirtualBox machine-folder configuration.
* `AD-LAB-NET` creation.
* VirtualBox DHCP disabled on the lab network.
* Creation of DC01.
* Creation of SRV01.
* Creation of PC01.
* Creation of PC02.
* CPU, RAM, network and VDI validation.

Formal evidence and repository documentation are being completed before B1 closure.
