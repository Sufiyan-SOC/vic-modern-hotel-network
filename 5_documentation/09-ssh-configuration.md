# SSH Configuration

The routers use local authentication and restrict VTY access to SSH:

```text
username sk password 0 sk
ip domain-name sk

line vty 0 4
 login local
 transport input ssh
```

The same VTY policy is present for lines `5 15`.

The required IT `Test-PC` is connected to **Fa0/2**, and its SSH remote-login test was completed.
