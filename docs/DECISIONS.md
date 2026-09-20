# AD-Lab — Technical Decisions

## Purpose

This document records significant technical and architectural decisions made during Active Directory Lab / AD-Lab.

Decisions should record not only what was selected, but why the choice exists and its consequences for later implementation.

---

## DEC-001 — Organization and Domain

**Status:** Accepted
**Block:** B0
**Date:** 2026-09-20

### Decision

Use:

```
Organization: ContosoLab
AD DNS Domain: ad.contosolab.test
NetBIOS: CONTOSOLAB
```

### Rationale

The laboratory requires a stable fictional organization and domain identity that can be reused consistently across Active Directory, DNS, DHCP, GPO, file services, documentation and troubleshooting scenarios.

### Consequences

All future domain-dependent configuration must use this identity unless a documented migration decision is made.

---

## DEC-002 — Initial Network

**Status:** Accepted
**Block:** B0
**Date:** 2026-09-20

### Decision

Use:

```
10.10.10.0/24
```

with:

```
Gateway: 10.10.10.1
DC01:    10.10.10.10
SRV01:   10.10.10.20
```

Planned DHCP pool:

```
10.10.10.100 - 10.10.10.199
```

### Rationale

A dedicated private `/24` provides sufficient capacity for the initial infrastructure and future laboratory expansion while remaining simple to diagnose and document.

### Consequences

Infrastructure services must respect the approved addressing plan.

---

## DEC-003 — Virtualization Platform

**Status:** Accepted
**Block:** B0 / B1
**Date:** 2026-09-20

### Decision

Use Oracle VirtualBox.

Validated implementation version:

```
7.2.18r175117
```

### Rationale

VirtualBox provides the required virtual machine and virtual networking capabilities for the laboratory.

### Consequences

VirtualBox commands and configuration form part of the reproducible laboratory setup.

---

## DEC-004 — Hyper-V and VBS Compatibility

**Status:** Accepted
**Block:** B1
**Date:** 2026-09-20

### Decision

Keep Windows Hyper-V-related functionality and Virtualization-Based Security enabled.

Do not disable these host security/virtualization capabilities merely to optimize VirtualBox.

### Evidence

VirtualBox validation confirmed:

```
Processor supports HW virtualization: yes
Processor supports nested paging: yes
```

and the required VM infrastructure could be created successfully.

### Consequences

If a later performance or compatibility issue occurs, it must be diagnosed using evidence before changing the host hypervisor/security configuration.

---

## DEC-005 — Operational Storage Separation

**Status:** Accepted
**Block:** B0 / B1
**Date:** 2026-09-20

### Decision

Separate operational infrastructure from the Git repository.

Operational laboratory:

```
D:\Labs\AD-Lab\
```

Git repository:

```
D:\Proyectos\AD-Lab\
```

### Rationale

Virtual disks, ISOs, backups and VM exports are operational artifacts and should not be stored in Git.

### Consequences

The repository contains documentation, scripts, configuration exports, diagrams and technical evidence only.

---

## DEC-006 — Dedicated VirtualBox NAT Network

**Status:** Accepted
**Block:** B1
**Date:** 2026-09-20

### Decision

Use:

```
AD-LAB-NET
10.10.10.0/24
Gateway 10.10.10.1
```

as the dedicated VirtualBox network for the initial AD-Lab systems.

### Consequences

DC01, SRV01, PC01 and PC02 use `AD-LAB-NET`.

---

## DEC-007 — Disable VirtualBox DHCP on AD-LAB-NET

**Status:** Accepted
**Block:** B1
**Date:** 2026-09-20

### Decision

VirtualBox DHCP remains disabled on `AD-LAB-NET`.

### Rationale

DHCP is a planned Windows Server laboratory service and must eventually be administered and validated from the Windows infrastructure rather than supplied transparently by VirtualBox.

### Consequences

The Windows DHCP role will later provide dynamic addressing to PC01 and PC02.

---

## DEC-008 — Active Directory Authorization Model

**Status:** Accepted
**Block:** B0
**Date:** 2026-09-20

### Decision

Use security groups and AGDLP where appropriate:

```
Accounts
  ↓
Global Groups
  ↓
Domain Local Groups
  ↓
Permissions
```

### Consequences

Direct assignment of file/resource permissions to individual users should be avoided unless specifically justified and documented.

---

## DEC-009 — Administrative Identity Separation

**Status:** Accepted
**Block:** B0
**Date:** 2026-09-20

### Decision

Standard user accounts use:

```
firstname.lastname
```

Administrative accounts use:

```
adm.firstname.lastname
```

Service identities use:

```
svc.<service>
```

### Rationale

Administrative and standard user identities should be distinguishable and follow least-privilege principles.

---

## DEC-010 — Evidence Format

**Status:** Accepted
**Block:** B0
**Date:** 2026-09-20

### Decision

Use Markdown as the standard textual evidence format.

Naming convention:

```
<DEVICE>-<BLOCK>-<DESCRIPTION>.md
```

### Required Content

Each textual evidence file should contain:

* Lab.
* Device.
* Block.
* Date.
* Objective.
* Commands.
* Relevant original output.
* PASS/FAIL result.
* Notes.

### Consequences

Raw textual validation evidence should be preserved when technically relevant instead of being replaced only by screenshots.

---

## DEC-011 — GitHub as Source of Truth

**Status:** Accepted / Pending Publication
**Block:** B0 / B1
**Date:** 2026-09-20

### Decision

GitHub will be the primary Source of Truth for:

* Documentation.
* Scripts.
* Configuration exports.
* Evidence.
* Diagrams.
* Decisions.
* Troubleshooting records.
* Project progress.

### Current State

The local repository has been initialized at:

```
D:\Proyectos\AD-Lab
```

GitHub publication has not yet been completed.

### Consequences

B1 must not claim GitHub Source of Truth establishment until the remote repository has actually been created, connected and verified.
