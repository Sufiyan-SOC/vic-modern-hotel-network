# DHCP Configuration

Each floor router acts as DHCP server for its local departments.

- F1: Reception, Store, Logistics
- F2: Finance, HR, Sales
- F3: IT, Admin

The supplied `show ip dhcp binding` output confirms active leases on multiple VLANs on every router. The F1 Store pool is configured but had zero leases in the supplied snapshot, so no successful Store client test is claimed here.
