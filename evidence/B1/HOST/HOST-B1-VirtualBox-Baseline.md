# HOST — B1 — VirtualBox Baseline

**LAB:** Active Directory Lab / AD-Lab
**DEVICE:** HOST
**BLOCK:** B1 — Virtualization Foundation
**DATE:** 2026-09-20

## Objective

Validate the host and Oracle VirtualBox baseline required to operate the AD-Lab virtual infrastructure.

Validation covers:

* VirtualBox version.
* Host operating system.
* Processor topology.
* Hardware virtualization.
* Nested paging.
* Host memory.
* VirtualBox default machine location.
* Extension Pack state.
* Compatibility with the Windows host virtualization configuration.

## Commands

```
VBoxManage --version
VBoxManage list hostinfo
VBoxManage list systemproperties
VBoxManage list extpacks
```

Additional Windows host validation performed during B1 included:

```
systeminfo
```

and inspection of the Windows hypervisor and Virtualization-Based Security state.

## Output

### VirtualBox

```
7.2.18r175117
```

VirtualBox was upgraded during B1 from:

```
6.1.50r161033
```

to:

```
7.2.18r175117
```

### Host

```
Processor online count: 12
Processor core count: 6
Processor supports HW virtualization: yes
Processor supports nested paging: yes
Memory size: 16106 MByte
Operating system: Windows 11
Operating system version: 10.0.26200.9457
```

Processor identified during the host baseline:

```
Intel Core i5-11400H @ 2.70GHz
```

### Windows Hypervisor / VBS

During B1 validation Windows reported that a hypervisor was detected and Virtualization-Based Security was running.

The validated configuration retained:

```
hypervisorlaunchtype On
```

Hyper-V-related functionality, Virtual Machine Platform, WSL and VBS were not disabled merely to favor VirtualBox.

### Default VirtualBox Machine Folder

Initial state:

```
D:\Máquinas virtuales\VritualBox\VB VMs
```

Configured state:

```
Default machine folder: D:\Labs\AD-Lab\VirtualMachines
```

### Extension Packs

```
Extension Packs: 0
```

## Result

**PASS**

Oracle VirtualBox 7.2.18 is operational.

The host provides:

* 6 physical processor cores.
* 12 logical processors.
* Hardware virtualization.
* Nested paging.
* Approximately 16 GB RAM.

The VirtualBox default machine directory is correctly configured as:

```
D:\Labs\AD-Lab\VirtualMachines
```

No Extension Pack is required for the current laboratory baseline.

## Notes

Host free memory varied during B1 depending on other applications running on Windows.

Before running multiple AD-Lab VMs simultaneously, available host memory should be checked.

An initial PowerShell registry inventory query generated an `InvalidCastException`. This affected only one evidence-collection method and not VirtualBox itself. VirtualBox CLI output and executable metadata were used to validate the installation instead.

The incident is recorded as `B1-INC-001` in `docs/TROUBLESHOOTING.md`.
