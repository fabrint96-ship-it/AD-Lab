# HOST — B1 — Virtual Machines

**LAB:** Active Directory Lab / AD-Lab
**DEVICE:** HOST
**BLOCK:** B1 — Virtualization Foundation
**DATE:** 2026-09-20

## Objective

Create and validate the initial AD-Lab virtual machines before guest operating-system installation.

Initial machines:

* DC01.
* SRV01.
* PC01.
* PC02.

## Commands

Final inventory:

```
VBoxManage list vms
VBoxManage list runningvms
```

Individual VM validation:

```
VBoxManage showvminfo <VM> --machinereadable
```

Virtual disk validation performed during B1:

```
VBoxManage showmediuminfo <VDI>
```

## Output

### Registered VMs

```
"DC01" {8039859b-d3f6-40c4-9b47-ab8c68e3108d}
"SRV01" {f4a382d7-c045-48c7-a430-7cabfebe96e9}
"PC01" {db3d48ae-009a-4555-b9a8-aaeec2960c8f}
"PC02" {0e44e7db-80ba-43b9-9374-1f1f0fcb9858}
```

### Running VMs

No virtual machines were running during final B1 validation.

### DC01

```
name="DC01"
ostype="Windows Server 2025 (64-bit)"
memory=3072
cpus=2
nat-network1="AD-LAB-NET"
nic1="natnetwork"
```

VM UUID:

```
8039859b-d3f6-40c4-9b47-ab8c68e3108d
```

Virtual disk:

```
UUID:       0b4dfd52-9de2-43ac-9150-18923e594eb9
Format:     VDI
Allocation: Dynamic
Capacity:   61440 MBytes
Initial physical size: 2 MBytes
```

### SRV01

```
name="SRV01"
ostype="Windows Server 2025 (64-bit)"
memory=3072
cpus=2
nat-network1="AD-LAB-NET"
nic1="natnetwork"
```

VM UUID:

```
f4a382d7-c045-48c7-a430-7cabfebe96e9
```

Virtual disk:

```
UUID:       100663d6-441c-4e2b-b8d9-be8146797bf4
Format:     VDI
Allocation: Dynamic
Capacity:   81920 MBytes
Initial physical size: 2 MBytes
```

### PC01

```
name="PC01"
ostype="Windows 11 (64-bit)"
memory=3072
cpus=2
nat-network1="AD-LAB-NET"
nic1="natnetwork"
```

VM UUID:

```
db3d48ae-009a-4555-b9a8-aaeec2960c8f
```

Virtual disk:

```
UUID:       ae481552-ade4-4697-9609-5506950bf281
Format:     VDI
Allocation: Dynamic
Capacity:   65536 MBytes
Initial physical size: 2 MBytes
```

### PC02

```
name="PC02"
ostype="Windows 11 (64-bit)"
memory=3072
cpus=2
nat-network1="AD-LAB-NET"
nic1="natnetwork"
```

VM UUID:

```
0e44e7db-80ba-43b9-9374-1f1f0fcb9858
```

Virtual disk:

```
UUID:       da857845-81b1-4324-8d08-5e99d7e8e266
Format:     VDI
Allocation: Dynamic
Capacity:   65536 MBytes
Initial physical size: 2 MBytes
```

## Validated VM Matrix

| VM    | Guest OS                | vCPU |     RAM |    VDI | Network    |
| ----- | ----------------------- | ---: | ------: | -----: | ---------- |
| DC01  | Windows Server 2025 x64 |    2 | 3072 MB | 60 GiB | AD-LAB-NET |
| SRV01 | Windows Server 2025 x64 |    2 | 3072 MB | 80 GiB | AD-LAB-NET |
| PC01  | Windows 11 x64          |    2 | 3072 MB | 64 GiB | AD-LAB-NET |
| PC02  | Windows 11 x64          |    2 | 3072 MB | 64 GiB | AD-LAB-NET |

All disks are dynamically allocated VDI images.

## Storage

VM directories:

```
D:\Labs\AD-Lab\VirtualMachines\DC01
D:\Labs\AD-Lab\VirtualMachines\SRV01
D:\Labs\AD-Lab\VirtualMachines\PC01
D:\Labs\AD-Lab\VirtualMachines\PC02
```

Supporting operational directories:

```
D:\Labs\AD-Lab\ISO
D:\Labs\AD-Lab\Backups
D:\Labs\AD-Lab\Exports
```

## Result

**PASS**

All four initial AD-Lab virtual machines:

* Exist.
* Are registered in VirtualBox.
* Use the approved guest OS type.
* Have 2 vCPUs.
* Have 3072 MB RAM.
* Use the approved VDI capacity.
* Use dynamically allocated VDI storage.
* Are connected to `AD-LAB-NET`.

No VM was running during the final B1 validation.

## Notes

No guest operating system has been installed as part of B1.

The very small initial physical size of the VDI files is expected because they use dynamic allocation.

The host does not need to run all four machines simultaneously.

A typical initial multi-machine scenario will use:

```
DC01 + SRV01 + PC01
```

representing approximately 9 GB of configured guest RAM.
