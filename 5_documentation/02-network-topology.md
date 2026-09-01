# Network Topology

```text
             F3-Router
             /       \
  10.10.10.0/30   10.10.10.4/30
         /             \
    F2-Router ------- F1-Router
          10.10.10.8/30
```

Each router connects to its floor switch through `Fa0/1` as an 802.1Q trunk. Department device ports are access ports assigned to their department VLAN.
