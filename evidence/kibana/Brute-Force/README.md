# Brute Force Evidence

## Objective

Document multiple failed authentication attempts identified during the attack simulation.

## Evidence

- Event ID 4625
- Failed logon attempts
- Elastic SIEM screenshots

## Detection Query

```kql
event.code:4625
```

## MITRE ATT&CK

- T1110 — Brute Force
