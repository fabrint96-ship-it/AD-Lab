# HOST — B1 — Virtual Network

**LAB:** Active Directory Lab / AD-Lab
**DEVICE:** HOST
**BLOCK:** B1 — Virtualization Foundation
**DATE:** 2026-09-20

## Objective

Create and validate the dedicated VirtualBox network used by AD-Lab.

The network must:

* Use `10.10.10.0/24`.
* Provide the planned `10.10.10.1` gateway.
* Provide controlled NAT connectivity.
* Connect the initial AD-Lab virtual machines.
* Not provide VirtualBox DHCP.
* Avoid conflicts with existing VirtualBox host-only infrastructure.

## Commands

Network inspection:

```
VBoxManage list natnets
VBoxManage list hostonlyifs
VBoxManage list dhcpservers
```

Network creation:

```
VBoxManage natnetwork add `
    --netname "AD-LAB-NET" `
    --network "10.10.10.0/24" `
    --enable `
    --dhcp off
```

Final validation:

```
VBoxManage list natnets
VBoxManage list dhcpservers
```

## Output

### Existing Host-Only Infrastructure

An existing VirtualBox Host-Only interface was detected using:

```
192.168.56.0/24
```

Host interface address:

```
192.168.56.1
```

An existing VirtualBox DHCP service was also identified for that Host-Only infrastructure:

```
NetworkName:    HostInterfaceNetworking-VirtualBox Host-Only Ethernet Adapter
Dhcpd IP:       192.168.56.100
LowerIPAddress: 192.168.56.101
UpperIPAddress: 192.168.56.254
NetworkMask:    255.255.255.0
Enabled:        Yes
```

This network does not overlap with AD-Lab.

### AD-LAB-NET Final Validation

```
Name:         AD-LAB-NET
Network:      10.10.10.0/24
Gateway:      10.10.10.1
DHCP Server:  No
IPv6:         No
IPv6 Prefix:  fd17:625c:f037:2::/64
IPv6 Default: No
```

Programmatic validation performed during B1 confirmed:

```
NetworkNameFound = True
NetworkCIDRFound = True
```

No VirtualBox DHCP server is enabled for `AD-LAB-NET`.

## Expected Future Network State

Infrastructure addressing:

```
Gateway   10.10.10.1
DC01      10.10.10.10
SRV01     10.10.10.20
```

Planned Windows DHCP range:

```
10.10.10.100 - 10.10.10.199
```

Planned Active Directory DNS:

```
10.10.10.10
```

## Result

**PASS**

The dedicated VirtualBox network exists with the approved configuration:

```
Name:      AD-LAB-NET
Network:   10.10.10.0/24
Gateway:   10.10.10.1
VBox DHCP: Disabled
```

The pre-existing `192.168.56.0/24` Host-Only infrastructure was left unchanged.

No address-space collision exists between the two networks.

## Notes

VirtualBox DHCP is deliberately disabled because Windows Server DHCP will later be implemented and validated as part of AD-Lab.

Domain clients will ultimately use DC01 as their DNS server rather than an external DNS resolver.

During inspection, `VBoxManage list hostonlynets` produced an unexpected unsupported/unknown-subcommand result. The required state was successfully established using `hostonlyifs`, `dhcpservers` and `natnets`.

The incident is documented as `B1-INC-002` in `docs/TROUBLESHOOTING.md`.
