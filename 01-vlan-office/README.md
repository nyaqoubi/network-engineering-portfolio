# Project 1 — VLAN Office Network

**Status:** Planned  
**Tool:** Cisco Packet Tracer

## Objective

Build a three-VLAN office network using 802.1Q trunking, inter-VLAN routing, and DHCP.

| VLAN | Department | Subnet | Gateway |
| --- | --- | --- | --- |
| 10 | Staff | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Guest | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Servers | 192.168.30.0/24 | 192.168.30.1 |

## Verification plan

- Check access port assignments with `show vlan brief`.
- Verify the trunk with `show interfaces trunk`.
- Check client leases with `show ip dhcp binding`.
- Test each client's gateway and inter-VLAN connectivity.

## Results

Pending lab implementation and testing.
