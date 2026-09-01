# Port Security

F3-Switch `Fa0/2` is the IT Test-PC access port.

Observed configuration:

```text
switchport access vlan 10
switchport mode access
switchport port-security
switchport port-security mac-address sticky
switchport port-security mac-address sticky 0090.0C7B.567B
```

Verified with `show port-security interface fa0/2`:

- Enabled: Yes
- Status: Secure-up
- Maximum MAC addresses: 1
- Sticky MAC addresses: 1
- Violation mode: Shutdown
- Violation count: 0
- Last source: `0090.0C7B.567B:10`
