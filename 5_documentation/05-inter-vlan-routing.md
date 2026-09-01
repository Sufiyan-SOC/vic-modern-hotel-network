# Inter-VLAN Routing

Router-on-a-stick is used. Each floor router's `GigabitEthernet0/0` is divided into 802.1Q subinterfaces.

Example:

```text
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.0
```

The same pattern is used for each departmental VLAN on the floor routers.
