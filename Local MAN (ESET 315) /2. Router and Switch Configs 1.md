# Router and Switch Configuration 1

## Overview
This lab focused on configuring and testing networks using basic networking commands. Task 1 used two routers, two switches, and four hosts to practice IP addressing and RIP routing. Task 2 involved configuring switch ports for VLAN 5 and testing network connectivity.

## Objectives
- Configure router interfaces with IP addresses and subnet masks.
- Configure RIP routing between routers.
- Assign IP addresses and default gateways to hosts.
- Configure switch ports for a VLAN.
- Verify network connectivity using `ping`, `tracert`, and router commands.
- Examine routing tables and interface status.

## Task 1: Router Configuration and RIP

### Network Topology
The first network consisted of two routers, two switches, and four hosts. The routers were connected to each other and to their respective switches, which connected to the hosts.

<img width="497" height="262" alt="R S Config 1 Setup" src="https://github.com/user-attachments/assets/9c772cfb-5483-41fd-b0cb-3132713f7fe5" />

### IP Addressing

| Device | Interface | IP Address | Default Gateway | Subnet |
|---|---|---|---|---|
| Router 1 | E0 | 20.20.1.1 | N/A | 20.20.1.0/24 |
| Router 1 | E1 | 30.30.30.1 | N/A | 30.30.30.0/24 |
| Router 2 | E0 | 40.40.70.1 | N/A | 40.40.70.0/24 |
| Router 2 | E1 | 30.30.30.2 | N/A | 30.30.30.0/24 |
| Laptop A1 | Ethernet | 20.20.1.2 | 20.20.1.1 | 20.20.1.0/24 |
| Host A2 | Ethernet | 20.20.1.3 | 20.20.1.1 | 20.20.1.0/24 |
| Host B1 | Ethernet | 40.40.70.2 | 40.40.70.1 | 40.40.70.0/24 |
| Host B2 | Ethernet | 40.40.70.3 | 40.40.70.1 | 40.40.70.0/24 |

### Router 1 Configuration

The report used the following interface configuration:

```text
en
conf t
interface eth0
ip address 20.20.1.1 255.255.255.0
no shutdown
interface eth1
ip address 30.30.30.1 255.255.255.0
no shutdown
```

### RIP Configuration

RIP was configured to advertise the networks connected to each router.

```text
router rip
network 20.20.1.0
network 30.30.30.0
```

The second router used the networks `30.30.30.0` and `40.40.70.0`.

### Connectivity Verification

After configuring the routers and hosts, connectivity was tested using `ping`. The `show ip route` command was used to inspect the routing table, and `show interfaces` was used to check interface status.

<img width="730" height="297" alt="image" src="https://github.com/user-attachments/assets/0953cf64-41f1-43e9-be8f-1b6a62a53d15" />
<img width="536" height="535" alt="image" src="https://github.com/user-attachments/assets/154ac9f0-ae88-48e2-801c-ba765df2ca05" />

The routing table displayed connected routes and RIP-learned routes. The report identified `C` as a connected route and `R` as a RIP route.

## Task 2: VLAN Configuration

### Switch Configuration

The second task used one switch with four connected ports assigned to VLAN 5. The switch was accessed through its console connection using PuTTY.

```text
enable
configure terminal

interface fa0/1
switchport access vlan 5

interface fa0/3
switchport access vlan 5

interface fa0/5
switchport access vlan 5

interface fa0/7
switchport access vlan 5
```

### Verification

The `show running-config` command was used to inspect the switch configuration. The `ping` command tested connectivity, while `tracert` displayed the route taken by packets.

<img width="556" height="850" alt="image" src="https://github.com/user-attachments/assets/9c1fc6c8-c83e-4423-97e0-a88ad1c9ebed" />
<img width="636" height="385" alt="image" src="https://github.com/user-attachments/assets/f72b83e7-eeca-4f46-a8c2-7fe8256a7829" />

## Key Takeaways
- Router interfaces need the correct IP addresses and subnet masks to communicate across networks.
- RIP allows routers to exchange routing information about reachable networks.
- Host default gateways provide a path to networks outside the local subnet.
- Switch access ports can be assigned to a specific VLAN.
- `ping`, `tracert`, `show ip route`, and `show interfaces` help verify connectivity and troubleshoot network configurations.

## Technologies and Tools
- Routers and Ethernet switches
- PuTTY
- IPv4 addressing and subnet masks
- RIP routing
- VLAN configuration
- `ping`
- `tracert`
- `show ip route`
- `show interfaces`
- `show running-config`
