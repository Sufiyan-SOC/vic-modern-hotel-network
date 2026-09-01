# Router Serial Links

| Network | Router | Interface | IP |
|---|---|---|---|
| 10.10.10.0/30 | F2 | S0/1/0 | 10.10.10.1 |
| 10.10.10.0/30 | F3 | S0/2/1 | 10.10.10.2 |
| 10.10.10.4/30 | F3 | S0/2/0 | 10.10.10.6 |
| 10.10.10.4/30 | F1 | S0/2/0 | 10.10.10.5 |
| 10.10.10.8/30 | F1 | S0/2/1 | 10.10.10.9 |
| 10.10.10.8/30 | F2 | S0/1/1 | 10.10.10.10 |

`clock rate 64000` is present on the DCE interfaces in the supplied configurations.
