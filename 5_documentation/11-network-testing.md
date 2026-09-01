
# 11. Network Testing

## Purpose

Network testing was performed to validate that the Vic Modern Hotel network operates as intended after configuration.

Testing focused on:

- Interface availability
- OSPF neighbor relationships
- OSPF route learning
- DHCP operation
- VLAN and trunk configuration
- SSH configuration
- Port security
- End-to-end IP connectivity

---

## 1. Router Interface Testing

The following command was used on each router:

```text
show ip interface brief
````

This command was used to verify:

* Router interface IP addresses
* Router subinterfaces
* Serial interface status
* Interface protocol state

The configured router subinterfaces and serial links were observed in an operational `up/up` state.

### Result

**PASS**

---

## 2. OSPF Neighbor Testing

The following command was used:

```text
show ip ospf neighbor
```

OSPF neighbor relationships were verified on all three floor routers.

The neighbors were reported in the:

```text
FULL
```

state.

### Verified OSPF Adjacencies

#### F1-Router

* Neighbor: `192.168.5.1`
* Neighbor: `192.168.2.1`

#### F2-Router

* Neighbor: `192.168.8.1`
* Neighbor: `192.168.2.1`

#### F3-Router

* Neighbor: `192.168.5.1`
* Neighbor: `192.168.8.1`

### Result

**PASS**

The FULL OSPF state confirms that OSPF adjacencies were successfully established between the floor routers.

---

## 3. OSPF Routing Table Testing

The following command was used:

```text
show ip route
```

Routes marked with:

```text
O
```

were used to identify networks learned through OSPF.

### F1-Router

The following remote networks were observed through OSPF:

* `192.168.1.0/24`
* `192.168.2.0/24`
* `192.168.3.0/24`
* `192.168.4.0/24`
* `192.168.5.0/24`

### F2-Router

The following remote networks were observed through OSPF:

* `192.168.1.0/24`
* `192.168.2.0/24`
* `192.168.6.0/24`
* `192.168.7.0/24`
* `192.168.8.0/24`

### F3-Router

The following remote networks were observed through OSPF:

* `192.168.3.0/24`
* `192.168.4.0/24`
* `192.168.5.0/24`
* `192.168.6.0/24`
* `192.168.7.0/24`
* `192.168.8.0/24`

### Result

**PASS**

The routing tables demonstrate that the floor routers are successfully exchanging and learning remote departmental networks using OSPF.

---

## 4. DHCP Testing

DHCP operation was checked using:

```text
show ip dhcp binding
```

and:

```text
show ip dhcp pool
```

These commands were used to verify:

* DHCP pool configuration
* Network ranges
* Default gateway configuration
* Number of leased addresses
* DHCP client assignments

### F1-Router DHCP Pools

Configured pools:

* Reception — `192.168.8.0/24`
* Store — `192.168.7.0/24`
* Logistics — `192.168.6.0/24`

Observed leases:

* Reception — 2
* Store — 0
* Logistics — 4

### F2-Router DHCP Pools

Configured pools:

* Finance — `192.168.5.0/24`
* HR — `192.168.4.0/24`
* Sales — `192.168.3.0/24`

Observed leases:

* Finance — 2
* HR — 2
* Sales — 3

### F3-Router DHCP Pools

Configured pools:

* IT — `192.168.1.0/24`
* Admin — `192.168.2.0/24`

Observed leases:

* IT — 2
* Admin — 1

### Result

**PASS**

DHCP operation was verified through the router DHCP binding tables and pool statistics.

---

## 5. VLAN Testing

VLAN configuration was verified using:

```text
show vlan brief
```

### F1-Switch

Verified departmental VLANs:

| VLAN | Department | Assigned Ports |
| ---: | ---------- | -------------- |
|   60 | Logistics  | Fa0/4–Fa0/8    |
|   70 | Store      | Configured     |
|   80 | Reception  | Fa0/2–Fa0/3    |

### F2-Switch

Verified departmental VLANs:

| VLAN | Department | Assigned Ports |
| ---: | ---------- | -------------- |
|   30 | Sales      | Fa0/6–Fa0/8    |
|   40 | HR         | Fa0/2–Fa0/3    |
|   50 | Finance    | Fa0/4–Fa0/5    |

### F3-Switch

Verified departmental VLANs:

| VLAN | Department | Assigned Ports |
| ---: | ---------- | -------------- |
|   10 | IT         | Fa0/2–Fa0/3    |
|   20 | Admin      | Fa0/4–Fa0/6    |

### Result

**PASS**

The departmental access ports were verified against their assigned VLANs.

---

## 6. Trunk Testing

The following command was used on each switch:

```text
show interfaces trunk
```

The floor uplinks were verified as IEEE 802.1Q trunks.

### Verified Trunk Ports

* F1-Switch — `Fa0/1`
* F2-Switch — `Fa0/1`
* F3-Switch — `Fa0/1`

The relevant departmental VLANs were shown as active on the trunk ports.

### Result

**PASS**

The switch-to-router uplinks are operating as 802.1Q trunks.

---

## 7. Port Security Testing

Port security was verified on the IT department switch.

The protected interface is:

```text
FastEthernet0/2
```

The following commands were used:

```text
show port-security
```

and:

```text
show port-security interface fa0/2
```

### Verified Configuration

```text
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Maximum MAC Addresses      : 1
Sticky MAC Addresses       : 1
Security Violation Count   : 0
```

The verified Test-PC MAC address is:

```text
0090.0C7B.567B
```

### Result

**PASS**

Port security is enabled on Fa0/2 with:

* Maximum of one secure MAC address
* Sticky MAC learning
* Shutdown violation mode
* Zero security violations observed

This matches the project requirement for the IT department Test-PC.

---

## 8. SSH Testing

SSH was configured on the floor routers using local authentication.

The router configuration includes:

```text
username sk password 0 sk
ip domain-name sk
```

The VTY lines were configured with:

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

The Test-PC connected to the IT department switch on:

```text
FastEthernet0/2
```

was used to perform the remote-login test.

### Result

**PASS**

The SSH remote-login test was successfully completed.

---

## 9. End-to-End Connectivity Testing

ICMP connectivity testing was performed from an end device using the Windows Command Prompt.

The following destinations were tested.

### Test 1 — HR Network

Command:

```text
ping 192.168.4.2
```

Observed result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### Result

**PASS**

The destination `192.168.4.2` responded successfully with 0% packet loss.

---

### Test 2 — Reception Network

Command:

```text
ping 192.168.8.2
```

Observed result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### Result

**PASS**

The destination `192.168.8.2` responded successfully with 0% packet loss.

---

### Test 3 — Admin Network

Command:

```text
ping 192.168.2.2
```

Observed result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### Result

**PASS**

The destination `192.168.2.2` responded successfully with 0% packet loss.

---

## 10. Connectivity Test Summary

| Test | Destination   | Network   | Packet Loss | Result |
| ---- | ------------- | --------- | ----------: | ------ |
| 1    | `192.168.4.2` | HR        |          0% | PASS   |
| 2    | `192.168.8.2` | Reception |          0% | PASS   |
| 3    | `192.168.2.2` | Admin     |          0% | PASS   |

The tested destinations successfully responded to ICMP requests.

---

## 11. Verification Summary

| Test Area               | Verification Method                  | Result |
| ----------------------- | ------------------------------------ | ------ |
| Router interfaces       | `show ip interface brief`            | PASS   |
| OSPF neighbors          | `show ip ospf neighbor`              | PASS   |
| OSPF routes             | `show ip route`                      | PASS   |
| DHCP bindings           | `show ip dhcp binding`               | PASS   |
| DHCP pools              | `show ip dhcp pool`                  | PASS   |
| VLAN configuration      | `show vlan brief`                    | PASS   |
| Trunk configuration     | `show interfaces trunk`              | PASS   |
| Port security           | `show port-security`                 | PASS   |
| Port security interface | `show port-security interface fa0/2` | PASS   |
| SSH                     | Remote-login test                    | PASS   |
| End-to-end connectivity | ICMP ping                            | PASS   |

---

## 12. Testing Evidence

The repository should include screenshots of the actual verification performed in Cisco Packet Tracer.

Recommended evidence includes:

* Router interface status
* OSPF neighbor status
* OSPF routing table
* DHCP bindings
* DHCP pool status
* VLAN configuration
* Trunk status
* Port-security status
* SSH remote-login test
* Successful ping tests

The screenshots should represent the actual Packet Tracer implementation and should be referenced from the project documentation where appropriate.

---

## 13. Conclusion

The network testing confirms that the major configured components of the Vic Modern Hotel network are functioning correctly in the Cisco Packet Tracer environment.

The collected verification evidence demonstrates working:

* VLAN segmentation
* Router-on-a-Stick inter-VLAN routing
* 802.1Q trunking
* OSPF routing
* DHCP services
* SSH remote access
* Switch port security
* End-to-end IP connectivity

