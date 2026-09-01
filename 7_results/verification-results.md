# Verification Results

## Overview

This document summarizes the verification performed on the Vic Modern Hotel network.

The verification is based on actual Cisco Packet Tracer command outputs collected from the three routers and three switches, along with the connectivity and SSH tests performed during the project.

No verification result is marked as completed unless supporting configuration output or an actual test result was available.

---

## 1. Router Interface Verification

### F1-Router

Command used:

```text
show ip interface brief
````

Verified interfaces:

| Interface             | IP Address  | Status | Protocol |
| --------------------- | ----------- | ------ | -------- |
| GigabitEthernet0/0.60 | 192.168.6.1 | up     | up       |
| GigabitEthernet0/0.70 | 192.168.7.1 | up     | up       |
| GigabitEthernet0/0.80 | 192.168.8.1 | up     | up       |
| Serial0/2/0           | 10.10.10.5  | up     | up       |
| Serial0/2/1           | 10.10.10.9  | up     | up       |

**Result: PASS**

---

### F2-Router

Command used:

```text
show ip interface brief
```

Verified interfaces:

| Interface             | IP Address  | Status | Protocol |
| --------------------- | ----------- | ------ | -------- |
| GigabitEthernet0/0.30 | 192.168.3.1 | up     | up       |
| GigabitEthernet0/0.40 | 192.168.4.1 | up     | up       |
| GigabitEthernet0/0.50 | 192.168.5.1 | up     | up       |
| Serial0/1/0           | 10.10.10.1  | up     | up       |
| Serial0/1/1           | 10.10.10.10 | up     | up       |

**Result: PASS**

---

### F3-Router

Command used:

```text
show ip interface brief
```

Verified interfaces:

| Interface             | IP Address  | Status | Protocol |
| --------------------- | ----------- | ------ | -------- |
| GigabitEthernet0/0.10 | 192.168.1.1 | up     | up       |
| GigabitEthernet0/0.20 | 192.168.2.1 | up     | up       |
| Serial0/2/0           | 10.10.10.6  | up     | up       |
| Serial0/2/1           | 10.10.10.2  | up     | up       |

**Result: PASS**

---

## 2. OSPF Verification

OSPF process `10` is configured on all three floor routers.

Command used:

```text
show ip ospf neighbor
```

### F1-Router OSPF Neighbors

| Neighbor Router ID | State | Neighbor Address |
| ------------------ | ----- | ---------------- |
| 192.168.5.1        | FULL  | 10.10.10.10      |
| 192.168.2.1        | FULL  | 10.10.10.6       |

### F2-Router OSPF Neighbors

| Neighbor Router ID | State | Neighbor Address |
| ------------------ | ----- | ---------------- |
| 192.168.8.1        | FULL  | 10.10.10.9       |
| 192.168.2.1        | FULL  | 10.10.10.2       |

### F3-Router OSPF Neighbors

| Neighbor Router ID | State | Neighbor Address |
| ------------------ | ----- | ---------------- |
| 192.168.5.1        | FULL  | 10.10.10.1       |
| 192.168.8.1        | FULL  | 10.10.10.5       |

The `FULL` state confirms that OSPF neighbor relationships were successfully established between the three routers.

**Result: PASS**

---

## 3. OSPF Route Verification

Command used:

```text
show ip route
```

OSPF-learned routes were identified using the `O` route code.

### F1-Router

The following remote networks were learned through OSPF:

* 192.168.1.0/24
* 192.168.2.0/24
* 192.168.3.0/24
* 192.168.4.0/24
* 192.168.5.0/24

### F2-Router

The following remote networks were learned through OSPF:

* 192.168.1.0/24
* 192.168.2.0/24
* 192.168.6.0/24
* 192.168.7.0/24
* 192.168.8.0/24

### F3-Router

The following remote networks were learned through OSPF:

* 192.168.3.0/24
* 192.168.4.0/24
* 192.168.5.0/24
* 192.168.6.0/24
* 192.168.7.0/24
* 192.168.8.0/24

The routing tables demonstrate that the floor routers are exchanging departmental networks using OSPF.

**Result: PASS**

---

## 4. VLAN Verification

VLAN configuration was verified on all three floor switches using:

```text
show vlan brief
```

### F1-Switch

| VLAN | Department | Verified Access Ports |
| ---: | ---------- | --------------------- |
|   60 | Logistics  | Fa0/4 - Fa0/8         |
|   70 | Store      | VLAN configured       |
|   80 | Reception  | Fa0/2 - Fa0/3         |

The switch also has Fa0/1 configured as the trunk uplink.

**Result: PASS**

---

### F2-Switch

| VLAN | Department | Verified Access Ports |
| ---: | ---------- | --------------------- |
|   30 | Sales      | Fa0/6 - Fa0/8         |
|   40 | HR         | Fa0/2 - Fa0/3         |
|   50 | Finance    | Fa0/4 - Fa0/5         |

The switch also has Fa0/1 configured as the trunk uplink.

**Result: PASS**

---

### F3-Switch

| VLAN | Department | Verified Access Ports |
| ---: | ---------- | --------------------- |
|   10 | IT         | Fa0/2 - Fa0/3         |
|   20 | Admin      | Fa0/4 - Fa0/6         |

The switch also has Fa0/1 configured as the trunk uplink.

**Result: PASS**

---

## 5. 802.1Q Trunk Verification

Command used:

```text
show interfaces trunk
```

### F1-Switch

Trunk interface:

```text
Fa0/1
```

Encapsulation:

```text
802.1q
```

Status:

```text
trunking
```

Active VLANs on the trunk:

```text
1, 60, 70, 80
```

**Result: PASS**

---

### F2-Switch

Trunk interface:

```text
Fa0/1
```

Encapsulation:

```text
802.1q
```

Status:

```text
trunking
```

Active VLANs on the trunk:

```text
1, 30, 40, 50
```

**Result: PASS**

---

### F3-Switch

Trunk interface:

```text
Fa0/1
```

Encapsulation:

```text
802.1q
```

Status:

```text
trunking
```

Active VLANs on the trunk:

```text
1, 10, 20
```

**Result: PASS**

---

## 6. DHCP Verification

DHCP configuration was verified using:

```text
show ip dhcp pool
```

and:

```text
show ip dhcp binding
```

Each floor router acts as the DHCP server for the VLANs located on its respective floor.

---

### F1-Router DHCP

Configured DHCP pools:

| Pool      | Network        | Default Gateway |
| --------- | -------------- | --------------- |
| Reception | 192.168.8.0/24 | 192.168.8.1     |
| Store     | 192.168.7.0/24 | 192.168.7.1     |
| Logistics | 192.168.6.0/24 | 192.168.6.1     |

Observed DHCP leases:

* Reception: 2
* Store: 0
* Logistics: 4

**Result: PASS**

The configured pools and active leases were verified.

---

### F2-Router DHCP

Configured DHCP pools:

| Pool    | Network        | Default Gateway |
| ------- | -------------- | --------------- |
| Finance | 192.168.5.0/24 | 192.168.5.1     |
| HR      | 192.168.4.0/24 | 192.168.4.1     |
| Sales   | 192.168.3.0/24 | 192.168.3.1     |

Observed DHCP leases:

* Finance: 2
* HR: 2
* Sales: 3

**Result: PASS**

---

### F3-Router DHCP

Configured DHCP pools:

| Pool  | Network        | Default Gateway |
| ----- | -------------- | --------------- |
| IT    | 192.168.1.0/24 | 192.168.1.1     |
| Admin | 192.168.2.0/24 | 192.168.2.1     |

Observed DHCP leases:

* IT: 2
* Admin: 1

**Result: PASS**

---

## 7. SSH Verification

SSH configuration was verified on the floor routers.

The routers contain local authentication configuration:

```text
username sk password 0 sk
```

Domain name configuration:

```text
ip domain-name sk
```

VTY configuration includes:

```text
line vty 0 4
 login local
 transport input ssh
```

and:

```text
line vty 5 15
 login local
 transport input ssh
```

The project requirement specifies that the IT Test-PC should be connected to:

```text
F3-Switch Fa0/2
```

The Test-PC was used to perform the remote SSH login test.

**Result: PASS**

The SSH remote-login test was successfully completed.

---

## 8. IT Department Port Security Verification

Port security was configured on:

```text
F3-Switch Fa0/2
```

The interface is assigned to:

```text
VLAN 10
```

The verified port-security status was:

```text
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Maximum MAC Addresses      : 1
Total MAC Addresses        : 1
Sticky MAC Addresses       : 1
Security Violation Count   : 0
```

The sticky MAC address learned for the Test-PC was:

```text
0090.0C7B.567B
```

The switch therefore allows one secure MAC address on Fa0/2 and uses shutdown mode for security violations.

**Result: PASS**

---

## 9. End-to-End Connectivity Verification

Connectivity testing was performed using ICMP ping from an end device.

### Test 1 — HR Network

Destination:

```text
192.168.4.2
```

Observed result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

**Result: PASS**

---

### Test 2 — Reception Network

Destination:

```text
192.168.8.2
```

Observed result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

**Result: PASS**

---

### Test 3 — Admin Network

Destination:

```text
192.168.2.2
```

Observed result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

**Result: PASS**

---

## 10. Connectivity Test Summary

| Test | Destination | Network   | Packet Loss | Result |
| ---- | ----------- | --------- | ----------: | ------ |
| 1    | 192.168.4.2 | HR        |          0% | PASS   |
| 2    | 192.168.8.2 | Reception |          0% | PASS   |
| 3    | 192.168.2.2 | Admin     |          0% | PASS   |

All three performed ping tests received four out of four ICMP replies.

---

## 11. Overall Verification Summary

| Component               | Verification              | Result |
| ----------------------- | ------------------------- | ------ |
| Router interfaces       | `show ip interface brief` | PASS   |
| VLAN configuration      | `show vlan brief`         | PASS   |
| 802.1Q trunking         | `show interfaces trunk`   | PASS   |
| OSPF neighbors          | `show ip ospf neighbor`   | PASS   |
| OSPF routing            | `show ip route`           | PASS   |
| DHCP pools              | `show ip dhcp pool`       | PASS   |
| DHCP leases             | `show ip dhcp binding`    | PASS   |
| SSH configuration       | Router configuration      | PASS   |
| SSH remote login        | Test-PC                   | PASS   |
| Port security           | `show port-security`      | PASS   |
| End-to-end connectivity | ICMP ping                 | PASS   |

---

## Conclusion

The collected verification evidence demonstrates that the major configured components of the Vic Modern Hotel network are operational in the Cisco Packet Tracer environment.

The verified implementation includes:

* Department-based VLAN segmentation
* Router-on-a-Stick inter-VLAN routing
* 802.1Q trunking
* OSPF dynamic routing
* DHCP services on the floor routers
* SSH remote management
* IT Test-PC connectivity
* Sticky MAC port security on F3-Switch Fa0/2
* End-to-end connectivity between tested networks

