# B1 — Virtualization Foundation

## Status

**CLOSED**

**Technical Validation:** PASS

## Objective

Build and validate the virtualization foundation required by Active Directory Lab / AD-Lab before guest operating-system installation and network configuration.

## Sections

| ID   | Section                                                    | Status    | Validation |
| ---- | ---------------------------------------------------------- | --------- | ---------- |
| B1.1 | VirtualBox Installation & Version Baseline                 | COMPLETED | PASS       |
| B1.2 | Hardware Virtualization & Hypervisor Compatibility         | COMPLETED | PASS       |
| B1.3 | AD-Lab Host Storage Preparation                            | COMPLETED | PASS       |
| B1.4 | VirtualBox Global Configuration                            | COMPLETED | PASS       |
| B1.5 | Virtual Network Preparation                                | COMPLETED | PASS       |
| B1.6 | VM Resource Templates & Creation Plan                      | COMPLETED | PASS       |
| B1.7 | Virtualization Validation                                  | COMPLETED | PASS       |
| B1.8 | Repository Bootstrap, Evidence, Documentation & B1 Closure | COMPLETED | PASS       |

## B1.1 — VirtualBox Baseline

Initial VirtualBox version:

```
6.1.50r161033
```

Final validated version:

```
7.2.18r175117
```

Extension Packs:

```
0
```

## B1.2 — Host Virtualization

Validated host:

```
Operating System: Windows 11
Version: 10.0.26200.9457
Processor cores: 6
Logical processors: 12
Memory: 16106 MByte
```

VirtualBox reported:

```
Processor supports HW virtualization: yes
Processor supports nested paging: yes
```

Windows Hyper-V/VBS functionality was retained.

No host security/virtualization capability was disabled merely to favor VirtualBox.

## B1.3 — Host Storage

Operational structure created under:

```
D:\Labs\AD-Lab
```

with:

```
Backups
Exports
ISO
VirtualMachines
VirtualMachines\DC01
VirtualMachines\SRV01
VirtualMachines\PC01
VirtualMachines\PC02
```

## B1.4 — VirtualBox Global Configuration

VirtualBox default machine folder changed from the previous host location to:

```
D:\Labs\AD-Lab\VirtualMachines
```

Final validation:

```
Default machine folder: D:\Labs\AD-Lab\VirtualMachines
```

## B1.5 — Virtual Network

Dedicated NAT Network:

```
Name:         AD-LAB-NET
Network:      10.10.10.0/24
Gateway:      10.10.10.1
DHCP Server:  No
IPv6:         No
```

VirtualBox DHCP was deliberately disabled.

An existing VirtualBox Host-Only network on `192.168.56.0/24` was left unchanged.

No address-space collision was identified.

## B1.6 — VM Resource Plan

| VM    | OS                      | vCPU |     RAM |    VDI |
| ----- | ----------------------- | ---: | ------: | -----: |
| DC01  | Windows Server 2025 x64 |    2 | 3072 MB | 60 GiB |
| SRV01 | Windows Server 2025 x64 |    2 | 3072 MB | 80 GiB |
| PC01  | Windows 11 x64          |    2 | 3072 MB | 64 GiB |
| PC02  | Windows 11 x64          |    2 | 3072 MB | 64 GiB |

All virtual disks use dynamic VDI allocation.

## B1.7 — Virtualization Validation

Registered VMs:

```
DC01
SRV01
PC01
PC02
```

All four machines were validated with:

```
cpus=2
memory=3072
nic1="natnetwork"
nat-network1="AD-LAB-NET"
```

No machines were running during final B1 validation.

No guest operating systems have been installed as part of B1.

## B1.8 — Repository & Evidence

Local Git repository:

```
D:\Proyectos\AD-Lab
```

Branch:

```
main
```

Remote repository:

```
https://github.com/fabrint96-ship-it/AD-Lab.git
```

B1 evidence:

```
evidence/B1/HOST/HOST-B1-VirtualBox-Baseline.md
evidence/B1/HOST/HOST-B1-Virtual-Network.md
evidence/B1/HOST/HOST-B1-Virtual-Machines.md
```

Troubleshooting incidents documented:

```
B1-INC-001
B1-INC-002
```

## Evidence

### VirtualBox / Host

```
evidence/B1/HOST/HOST-B1-VirtualBox-Baseline.md
```

### Network

```
evidence/B1/HOST/HOST-B1-Virtual-Network.md
```

### Virtual Machines

```
evidence/B1/HOST/HOST-B1-Virtual-Machines.md
```

## Validation Result

**PASS**

The virtualization foundation required for AD-Lab exists and has been technically validated.

Validated state:

* VirtualBox operational.
* Hardware virtualization available.
* Operational storage prepared.
* VirtualBox VM location configured.
* Dedicated NAT Network created.
* VirtualBox DHCP disabled.
* Four initial VMs created.
* VM resources validated.
* Virtual disks validated.
* Network attachment validated.

## Final Closure

Implementation: PASS  
Validation: PASS  
Evidence: PASS  
Documentation: PASS  
Git record: PASS  
GitHub publication: PASS

Validated baseline before closure documentation:

```
eff95cdf16eada778ed91606abf3a7d9b9496608
```

At that checkpoint, local `HEAD`, local `main` and `origin/main` were verified to reference the same commit.

**B1 — Virtualization Foundation is formally CLOSED.**

Next block:

```
B2 — Network Foundation
```

## Result

**PASS — CLOSED**

B1 has completed implementation, verification, evidence capture, documentation, review, recording and formal closure.
