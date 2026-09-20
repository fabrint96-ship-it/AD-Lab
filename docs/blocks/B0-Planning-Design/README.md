# B0 — Planning & Design

## Status

**CLOSED**

**Validation:** PASS

## Objective

Define the architectural, organizational and operational baseline of Active Directory Lab / AD-Lab before creating the infrastructure.

B0 establishes the decisions that subsequent implementation blocks must follow.

No Windows Server installation or Active Directory deployment is performed in this block.

## Sections

| ID   | Section                                                                        | Status    |
| ---- | ------------------------------------------------------------------------------ | --------- |
| B0.1 | Scope, Organization, Naming, Domain, Machines, IP Addressing & Topology Design | COMPLETED |
| B0.2 | Virtualization Platform & Host Resource Planning                               | COMPLETED |
| B0.3 | Active Directory Logical Design                                                | COMPLETED |
| B0.4 | Repository, Documentation & Evidence Design                                    | COMPLETED |
| B0.5 | Implementation Roadmap, Validation Matrix & B0 Closure                         | COMPLETED |

## B0.1 — Scope & Infrastructure Design

Approved laboratory:

```
Active Directory Lab / AD-Lab
```

Organization:

```
ContosoLab
```

Active Directory DNS domain:

```
ad.contosolab.test
```

NetBIOS:

```
CONTOSOLAB
```

Initial systems:

```
DC01
SRV01
PC01
PC02
```

Network:

```
10.10.10.0/24
```

Planned addressing:

```
Gateway    10.10.10.1
DC01       10.10.10.10
SRV01      10.10.10.20
DNS        10.10.10.10
```

Planned DHCP range:

```
10.10.10.100 - 10.10.10.199
```

PC01 and PC02 will use DHCP.

## B0.2 — Virtualization Planning

Selected platform:

```
Oracle VirtualBox
```

Approved initial VM resources:

| VM    | vCPU |  RAM |  Disk |
| ----- | ---: | ---: | ----: |
| DC01  |    2 | 3 GB | 60 GB |
| SRV01 |    2 | 3 GB | 80 GB |
| PC01  |    2 | 3 GB | 64 GB |
| PC02  |    2 | 3 GB | 64 GB |

Operational storage:

```
D:\Labs\AD-Lab
```

VirtualBox network:

```
AD-LAB-NET
```

Planned snapshot checkpoints:

```
S00-Clean-Install
S01-Network-Configured
S02-Before-ADDS
S03-ADDS-Operational
S04-Before-GPO
```

## B0.3 — Active Directory Logical Design

Initial architecture:

```
1 Forest
1 Domain
```

Domain:

```
ad.contosolab.test
```

Initial OU design:

```
ContosoLab
├── Users
│   ├── Direction
│   ├── IT
│   ├── Administration
│   ├── HR
│   ├── Finance
│   ├── Sales
│   └── Support
├── Computers
│   ├── Workstations
│   └── Laptops
├── Servers
├── Service Accounts
└── Disabled Objects
```

Initial global security groups:

```
GG_Direction
GG_IT
GG_Administration
GG_HR
GG_Finance
GG_Sales
GG_Support
```

Authorization model:

```
Accounts
  ↓
Global Groups
  ↓
Domain Local Groups
  ↓
Permissions
```

AGDLP will be used where appropriate.

## B0.4 — Repository & Evidence Design

Repository:

```
AD-Lab
```

Primary branch:

```
main
```

Local repository location:

```
D:\Proyectos\AD-Lab
```

GitHub is intended to become the project Source of Truth after remote publication.

Textual evidence format:

```
Markdown (.md)
```

Naming:

```
<DEVICE>-<BLOCK>-<DESCRIPTION>.md
```

Operational infrastructure is deliberately excluded from Git.

## B0.5 — Roadmap

Approved implementation sequence:

```
B0  Planning & Design
B1  Virtualization Foundation
B2  Network Foundation
B3  Windows Server Foundation
B4  Active Directory Deployment
B5  DNS
B6  DHCP
B7  OU, Users & Groups
B8  Windows Clients
B9  Group Policy
B10 File Server & Permissions
B11 PowerShell Automation
B12 Security Hardening
B13 Monitoring & Auditing
B14 Troubleshooting Scenarios
B15 Backup & Recovery
B16 Final Validation
B17 GitHub Documentation & Portfolio
```

## Validation

B0 was reviewed before infrastructure implementation began.

The following were established before B1:

* Scope.
* Organization.
* Domain.
* Naming.
* Machines.
* Network.
* Addressing.
* Virtualization platform.
* Resource plan.
* AD logical design.
* Repository model.
* Evidence model.
* Implementation roadmap.

## Result

**PASS**

B0 established a sufficient design baseline to begin implementation without requiring an infrastructure redesign.

## Closure

**B0 — Planning & Design: CLOSED**
