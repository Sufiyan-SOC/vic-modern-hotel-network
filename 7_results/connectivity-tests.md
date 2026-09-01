# Connectivity Tests

## Overview

This document records the connectivity tests performed on the Vic Modern Hotel network.

The tests were performed from an end device using the Windows Command Prompt in Cisco Packet Tracer.

The purpose of the tests was to verify end-to-end communication between devices belonging to different VLANs and different floors.

---

## Test Environment

- Project: Vic Modern Hotel Network
- Simulation Tool: Cisco Packet Tracer
- Routing Protocol: OSPF
- Inter-VLAN Routing: Router-on-a-Stick
- DHCP: Configured on floor routers
- VLANs: 10, 20, 30, 40, 50, 60, 70, 80

---

## Connectivity Test Results

### Test 1 — Cross-VLAN Connectivity

**Destination:** `192.168.4.2`


C:\>ping 192.168.4.2

Pinging 192.168.4.2 with 32 bytes of data:
Reply from 192.168.4.2: bytes=32 time=1ms TTL=126
Reply from 192.168.4.2: bytes=32 time=1ms TTL=126
Reply from 192.168.4.2: bytes=32 time=1ms TTL=126
Reply from 192.168.4.2: bytes=32 time=1ms TTL=126

Ping statistics for 192.168.4.2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)


**Result: PASS**

The destination responded successfully with 0% packet loss.

This demonstrates successful IP connectivity to the `192.168.4.0/24` network.

---

### Test 2 — Connectivity to First-Floor Network

**Destination:** `192.168.8.2`


C:\>ping 192.168.8.2

Pinging 192.168.8.2 with 32 bytes of data:
Reply from 192.168.8.2: bytes=32 time=1ms TTL=126
Reply from 192.168.8.2: bytes=32 time=2ms TTL=126
Reply from 192.168.8.2: bytes=32 time=1ms TTL=126
Reply from 192.168.8.2: bytes=32 time=23ms TTL=126

Ping statistics for 192.168.8.2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)


**Result: PASS**

The destination responded successfully with 0% packet loss.

This verifies connectivity to the Reception VLAN network (`192.168.8.0/24`).

---

### Test 3 — Connectivity to Third-Floor Admin Network

**Destination:** `192.168.2.2`


C:\>ping 192.168.2.2

Pinging 192.168.2.2 with 32 bytes of data:
Reply from 192.168.2.2: bytes=32 time<1ms TTL=127
Reply from 192.168.2.2: bytes=32 time<1ms TTL=127
Reply from 192.168.2.2: bytes=32 time<1ms TTL=127
Reply from 192.168.2.2: bytes=32 time<1ms TTL=127

Ping statistics for 192.168.2.2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)


**Result: PASS**

The destination responded successfully with 0% packet loss.

This verifies connectivity to the Admin VLAN network (`192.168.2.0/24`).

---

## Summary

| Test | Destination   | Network        | Result |
| ---- | ------------- | -------------- | ------ |
| 1    | `192.168.4.2` | HR VLAN        | PASS   |
| 2    | `192.168.8.2` | Reception VLAN | PASS   |
| 3    | `192.168.2.2` | Admin VLAN     | PASS   |

All three tested destinations returned successful ICMP replies with **0% packet loss**.

These tests provide evidence that routing between the tested networks is functioning correctly.



