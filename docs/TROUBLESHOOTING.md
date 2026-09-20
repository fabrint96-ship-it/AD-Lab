# AD-Lab — Troubleshooting Register

## 1. Purpose

This document records relevant incidents encountered during Active Directory Lab / AD-Lab.

Troubleshooting is treated as part of the laboratory evidence rather than as undocumented trial and error.

Each relevant incident should record:

* Symptom.
* Expected state.
* Hypotheses.
* Diagnosis.
* Commands or tools used.
* Root cause.
* Resolution.
* Validation.
* Prevention or lesson learned.

---

# B1 Incidents

## B1-INC-001 — VirtualBox Registry Inventory Query Failure

**Block:** B1 — Virtualization Foundation
**Status:** RESOLVED
**Impact:** Evidence collection only
**Infrastructure impact:** None

### Symptom

During the initial VirtualBox installation baseline, a PowerShell registry inventory query generated an `InvalidCastException`.

The query was intended to retrieve installed VirtualBox package/version metadata.

### Expected State

The evidence collection command should return the installed Oracle VirtualBox product and version information without error.

### Impact Assessment

The failure did not indicate that VirtualBox itself was malfunctioning.

VirtualBox command-line tools remained operational.

The issue affected only one method used to collect installation metadata.

### Diagnosis

VirtualBox installation and version information were independently available from:

```
VBoxManage --version
```

and from executable file metadata.

The initial VirtualBox version was established as:

```
6.1.50r161033
```

Executable metadata reported:

```
ProductVersion: 6.1.50.161033
FileVersion:    6.1.50.161033
```

### Root Cause

The PowerShell registry inventory command attempted an incompatible value/type conversion while processing registry data.

The failure was associated with the evidence collection method rather than the VirtualBox installation.

### Resolution

The registry query was not used as the authoritative validation method.

VirtualBox CLI output and executable metadata were used instead.

VirtualBox was subsequently upgraded and validated as:

```
7.2.18r175117
```

### Validation

Command:

```
VBoxManage --version
```

Final output:

```
7.2.18r175117
```

Additional host and VM validation completed successfully.

### Result

**RESOLVED / PASS**

### Prevention / Lesson Learned

Do not rely on a single Windows registry query as the sole source for installed application version evidence.

Prefer application-native CLI version output when available and corroborate with executable metadata when necessary.

---

## B1-INC-002 — `hostonlynets` Subcommand Inconsistency

**Block:** B1 — Virtualization Foundation
**Status:** RESOLVED / NON-BLOCKING
**Impact:** Evidence collection only
**Infrastructure impact:** None

### Symptom

During VirtualBox networking inspection:

```
VBoxManage list hostonlynets
```

returned an unknown-subcommand error even though related help information indicated host-only networking functionality.

### Expected State

The command was expected to list host-only network configuration.

### Diagnosis

Required network information remained available through:

```
VBoxManage list hostonlyifs
```

and:

```
VBoxManage list dhcpservers
```

These commands identified the existing host-only interface and its associated DHCP configuration.

The existing host-only network used:

```
192.168.56.0/24
```

The dedicated AD-Lab network uses:

```
10.10.10.0/24
```

No address-space conflict existed.

### Resolution

The unsupported/inconsistent command was not required for implementation.

Alternative VirtualBox queries provided the information required for network validation.

### Validation

`AD-LAB-NET` was independently validated using:

```
VBoxManage list natnets
```

with:

```
Name:         AD-LAB-NET
Network:      10.10.10.0/24
Gateway:      10.10.10.1
DHCP Server:  No
```

### Result

**RESOLVED / PASS**

### Prevention / Lesson Learned

Use the commands supported by the installed VirtualBox version rather than assuming every documented or help-listed networking query behaves identically across versions.

Validate the required state through alternative authoritative commands when a non-essential inspection command is unavailable.

---

# Future Incident Template

## <INCIDENT-ID> — <Title>

**Block:**
**Status:**
**Impact:**

### Symptom

Describe what was observed.

### Expected State

Describe what should have happened.

### Hypotheses

Record plausible causes before making corrective changes.

### Diagnosis

Record commands, logs, tests and observations used to isolate the problem.

### Root Cause

Record the demonstrated cause.

### Resolution

Record the corrective action.

### Validation

Record how the corrected state was verified.

### Result

**PASS / FAIL**

### Prevention / Lesson Learned

Record how the issue could be prevented, detected earlier or diagnosed more efficiently.
