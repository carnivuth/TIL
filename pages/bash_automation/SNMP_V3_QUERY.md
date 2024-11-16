---
index: 5
---
# HOW TO QUERY A SNMP V3 CAPABLE DEVICE

```bash
snmpwalk -v3 -u [user] -l authNoPriv -a md5 -A [community] [node] [oid]
```
