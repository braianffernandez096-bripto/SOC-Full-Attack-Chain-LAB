# Brute Force Evidence

## Objective

Document brute-force authentication attempts and the resulting account lockout.

## Evidence

- Event ID 4625 — Multiple failed authentication attempts.
- Event ID 4740 — User account locked after exceeding the configured threshold.

## Detection Queries

```kql
event.code:4625
```

```kql
event.code:4740
```

## MITRE ATT&CK

- T1110 — Brute Force

## Observation

The account lockout event confirms that the configured security policy successfully mitigated the brute-force attack by temporarily preventing additional authentication attempts.
