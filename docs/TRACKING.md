# AD-Lab — Project Tracking

## 1. Purpose

This document is the authoritative progress register for Active Directory Lab / AD-Lab.

A block is not considered `CLOSED` until its required implementation, validation, evidence and documentation have been completed.

## 2. States

The project uses the following states:

| State       | Meaning                                                               |
| ----------- | --------------------------------------------------------------------- |
| NOT STARTED | Work has not begun                                                    |
| PLANNING    | Scope or design is being defined                                      |
| READY       | Planning is complete and implementation can begin                     |
| IN PROGRESS | Implementation is underway                                            |
| BLOCKED     | Progress cannot continue because of an unresolved dependency or issue |
| VALIDATING  | Implementation exists and is being technically verified               |
| DOCUMENTING | Validation passed and evidence/documentation is being completed       |
| COMPLETED   | Required implementation, validation and documentation are complete    |
| CLOSED      | Block has passed final review and has been formally recorded          |

## 3. Project Status

**Project:** Active Directory Lab / AD-Lab  
**Organization:** ContosoLab  
**Domain:** `ad.contosolab.test`

**Current block:** B2 — Network Foundation  
**Current state:** NOT STARTED

## 4. Block Tracking

| ID  | Block                            | State       | Validation | Evidence                                 |
| --- | -------------------------------- | ----------- | ---------- | ---------------------------------------- |
| B0  | Planning & Design                | CLOSED      | PASS       | Design recorded in project documentation |
| B1  | Virtualization Foundation        | CLOSED      | PASS       | PASS — B1 evidence stored in repository  |
| B2  | Network Foundation               | NOT STARTED | —          | —                                        |
| B3  | Windows Server Foundation        | NOT STARTED | —          | —                                        |
| B4  | Active Directory Deployment      | NOT STARTED | —          | —                                        |
| B5  | DNS                              | NOT STARTED | —          | —                                        |
| B6  | DHCP                             | NOT STARTED | —          | —                                        |
| B7  | OU, Users & Groups               | NOT STARTED | —          | —                                        |
| B8  | Windows Clients                  | NOT STARTED | —          | —                                        |
| B9  | Group Policy                     | NOT STARTED | —          | —                                        |
| B10 | File Server & Permissions        | NOT STARTED | —          | —                                        |
| B11 | PowerShell Automation            | NOT STARTED | —          | —                                        |
| B12 | Security Hardening               | NOT STARTED | —          | —                                        |
| B13 | Monitoring & Auditing            | NOT STARTED | —          | —                                        |
| B14 | Troubleshooting Scenarios        | NOT STARTED | —          | —                                        |
| B15 | Backup & Recovery                | NOT STARTED | —          | —                                        |
| B16 | Final Validation                 | NOT STARTED | —          | —                                        |
| B17 | GitHub Documentation & Portfolio | NOT STARTED | —          | —                                        |

## 5. B0 — Planning & Design

**State:** CLOSED  
**Validation:** PASS

| Section | Description                                                                    | State     |
| ------- | ------------------------------------------------------------------------------ | --------- |
| B0.1    | Scope, Organization, Naming, Domain, Machines, IP Addressing & Topology Design | COMPLETED |
| B0.2    | Virtualization Platform & Host Resource Planning                               | COMPLETED |
| B0.3    | Active Directory Logical Design                                                | COMPLETED |
| B0.4    | Repository, Documentation & Evidence Design                                    | COMPLETED |
| B0.5    | Implementation Roadmap, Validation Matrix & B0 Closure                         | COMPLETED |

### B0 Result

The initial project architecture was defined before infrastructure implementation.

Key decisions include:

* Organization: `ContosoLab`.
* Domain: `ad.contosolab.test`.
* NetBIOS: `CONTOSOLAB`.
* Network: `10.10.10.0/24`.
* Virtualization: Oracle VirtualBox.
* Initial systems: DC01, SRV01, PC01 and PC02.
* GitHub is the project Source of Truth for recorded project state.

## 6. B1 — Virtualization Foundation

**State:** CLOSED  
**Technical validation:** PASS  
**Evidence:** PASS  
**Documentation:** PASS  
**Git record:** PASS  
**GitHub publication:** PASS

| Section | Description                                                | State     | Validation |
| ------- | ---------------------------------------------------------- | --------- | ---------- |
| B1.1    | VirtualBox Installation & Version Baseline                 | COMPLETED | PASS       |
| B1.2    | Hardware Virtualization & Hypervisor Compatibility         | COMPLETED | PASS       |
| B1.3    | AD-Lab Host Storage Preparation                            | COMPLETED | PASS       |
| B1.4    | VirtualBox Global Configuration                            | COMPLETED | PASS       |
| B1.5    | Virtual Network Preparation                                | COMPLETED | PASS       |
| B1.6    | VM Resource Templates & Creation Plan                      | COMPLETED | PASS       |
| B1.7    | Virtualization Validation                                  | COMPLETED | PASS       |
| B1.8    | Repository Bootstrap, Evidence, Documentation & B1 Closure | COMPLETED | PASS       |

### B1 Technical State

Validated:

* Oracle VirtualBox `7.2.18r175117`.
* Windows 11 host.
* Hardware virtualization available.
* Nested paging available.
* Hyper-V/VBS compatibility retained.
* Operational storage under `D:\Labs\AD-Lab`.
* VirtualBox default VM folder configured.
* `AD-LAB-NET` created.
* Network `10.10.10.0/24`.
* Gateway `10.10.10.1`.
* VirtualBox DHCP disabled on `AD-LAB-NET`.
* DC01 created and validated.
* SRV01 created and validated.
* PC01 created and validated.
* PC02 created and validated.
* All four VMs attached to `AD-LAB-NET`.

### B1 Closure Requirements

* [x] Virtualization implementation completed.
* [x] Technical validation passed.
* [x] Local Git repository initialized.
* [x] Repository structure created.
* [x] B1 evidence files stored.
* [x] Core documentation completed.
* [x] Repository review completed.
* [x] Initial Git record created.
* [x] GitHub remote repository created and verified.
* [x] B1 final checkpoint recorded.

### B1 Final Checkpoint

Initial published and validated baseline:

```
eff95cdf16eada778ed91606abf3a7d9b9496608
```

At this checkpoint, local `HEAD`, local `main` and `origin/main` were verified to reference the same commit before the B1 closure-documentation update.

**B1 — Virtualization Foundation: CLOSED**

## 7. Next Block

**B2 — Network Foundation**

State:

```
NOT STARTED
```

B1 is formally closed and B2 may now begin.
