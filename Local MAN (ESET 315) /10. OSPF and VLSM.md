# Lab 12: Variable Length Subnet Masking (VLSM) and Open Shortest Path First (OSPF)

## Overview
This lab focused on implementing Variable Length Subnet Masking (VLSM) and configuring Open Shortest Path First (OSPF) routing. We calculated subnet addresses for networks with different host requirements, assigned IP addresses to routers and hosts, and examined routing tables to understand how OSPF distributes routes throughout a network.

We also used traceroute to verify connectivity between student laptops across the network.

## Objectives
- Calculate VLSM subnet addresses based on host requirements.
- Determine subnet masks, usable IP ranges, and broadcast addresses.
- Assign IP addresses to router interfaces and hosts.
- Configure and examine OSPF routing.
- Analyze routing tables using `show ip route`.
- Identify directly connected, OSPF-learned, and static routes.
- Verify connectivity using `traceroute`.

## Network Topology

The network consisted of four routers and student laptops connected through multiple subnets. Different subnet sizes were assigned based on the number of hosts required for each network.

<img width="754" height="531" alt="image" src="https://github.com/user-attachments/assets/8062b8bb-081b-4651-bc18-f731ab81b224" />

## IP Addressing

### VLSM Subnet Assignment

Five subnets were calculated using the `200.0.0.0` address space. Each subnet was assigned a mask based on its host requirements.

| Subnet | Network Address | Subnet Mask | Prefix | First Usable Address | Last Usable Address | Broadcast Address |
|---|---|---|---|---|---|---|
| Subnet 1 — 90 hosts | 200.0.0.0 | 255.255.255.128 | /25 | 200.0.0.1 | 200.0.0.126 | 200.0.0.127 |
| Subnet 2 — 40 hosts | 200.0.0.128 | 255.255.255.192 | /26 | 200.0.0.129 | 200.0.0.190 | 200.0.0.191 |
| Subnet 3 — 25 hosts | 200.0.0.192 | 255.255.255.224 | /27 | 200.0.0.193 | 200.0.0.222 | 200.0.0.223 |
| Subnet 4 — R1, R2, R4 | 200.0.0.224 | 255.255.255.248 | /29 | 200.0.0.225 | 200.0.0.230 | 200.0.0.231 |
| Subnet 5 — R2, R3 | 200.0.0.232 | 255.255.255.252 | /30 | 200.0.0.233 | 200.0.0.234 | 200.0.0.235 |

### Router and Host IP Assignments

IP addresses were assigned to the router interfaces and student laptops according to the network diagram.

**Network Diagram with IP Address Assignments**

<img width="777" height="465" alt="image" src="https://github.com/user-attachments/assets/b91df871-0cbf-4561-a5a6-9d24ecb6ff84" />

The original report references the completed network diagram for the individual interface assignments. The full device-by-device IP assignment table was not included in the supplied text.

## Configuration and Testing

### OSPF Routing
OSPF was used to exchange routing information between routers. We examined the routing tables of all four routers to identify directly connected networks, routes learned through OSPF, and manually configured static routes.

The following command was used to inspect the routing tables:

```text
show ip route
```

### Routing Table Analysis

The routing tables displayed route codes identifying how each network was reached.

| Route Code | Meaning | Description |
|---|---|---|
| `C` | Connected | The subnet is directly connected to the router. |
| `O` | OSPF | The subnet was learned through OSPF routing. |
| `S*` | Candidate default route | The default route was manually configured as a static route. |

### Router 1

Router 1 had two directly connected subnets marked with `C`. The remaining `O` routes were learned through OSPF and were routed through interface E1. A static default route was also configured.

**Figure 2: Router 1 Routing Table**

<img width="706" height="356" alt="image" src="https://github.com/user-attachments/assets/72e8a319-cb33-48ab-8026-7c47e79d8f37" />

### Router 2

Router 2 had three directly connected subnets marked with `C`. The remaining `O` routes were learned through OSPF, with routes using different interfaces, including S0 and E0. A static default route was also configured.

**Figure 3: Router 2 Routing Table**

<img width="667" height="341" alt="image" src="https://github.com/user-attachments/assets/f97bc6aa-dc47-4468-a103-caa8ecbc551e" />

### Router 3

Router 3 had two directly connected subnets marked with `C`. The remaining `O` routes were learned through OSPF and were routed through interface S1. A static default route was also configured.

**Figure 4: Router 3 Routing Table**

<img width="680" height="342" alt="image" src="https://github.com/user-attachments/assets/7df32b3e-887a-4454-929d-440b77456dd8" />

### Router 4

Router 4 had two directly connected subnets marked with `C`. The remaining `O` routes were learned through OSPF and were routed through interface E0.

Unlike the other three routers, Router 4 did not have a manually configured static default route because it served as the default route in the network.

**Figure 5: Router 4 Routing Table**

<img width="668" height="303" alt="image" src="https://github.com/user-attachments/assets/4a1d8301-b3ff-4f48-84dd-b73ce292b8ad" />

## Traceroute Verification

Traceroute was used to verify connectivity between student laptops across the network. Laptop of Student #2 was used as the destination representing the Internet for these tests.

The report required traceroute screenshots for the following paths:

### Student #1 to Student #2

<img width="600" height="249" alt="image" src="https://github.com/user-attachments/assets/eaf834e1-a1fb-422d-9d60-aa9bb57bb590" />


### Student #4 to Student #2

<img width="594" height="266" alt="image" src="https://github.com/user-attachments/assets/3ce5aa27-6621-4ec9-b73d-23be2f7a0ba6" />

### Student #3 to Student #2

<img width="719" height="114" alt="image" src="https://github.com/user-attachments/assets/03d58e57-f0d8-4693-808e-d2b40b16248d" />

## Key Takeaways
- VLSM allows networks with different host requirements to use appropriately sized subnets.
- The subnet mask determines the size of each subnet and the number of usable host addresses.
- OSPF allows routers to learn routes to networks that are not directly connected.
- The `C` route code identifies directly connected networks, while `O` identifies OSPF-learned routes.
- Static default routes can be used to direct traffic toward a default destination.
- Routing tables help identify the interfaces used to reach different subnets.
- Traceroute helps verify connectivity and observe the path packets take through the network.

## Technologies and Tools
- Cisco routers
- Cisco IOS CLI
- Variable Length Subnet Masking (VLSM)
- Open Shortest Path First (OSPF)
- IPv4 subnetting
- `show ip route`
- `traceroute`
