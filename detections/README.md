# Detection Rules

This directory contains the detection queries used throughout the investigation.

The rules were created to identify each stage of the simulated attack and are based on Windows Security Events and Sysmon telemetry.

## Detection Coverage

| Attack Phase | Detection |
|--------------|-----------|
| Brute Force | Event ID 4625 |
| Initial Access | Event ID 4624 |
| Privilege Escalation | Event ID 4672 |
| Persistence | Event IDs 4720 / 4732 |
| Remote Execution | Event IDs 7045 / 4688 |

These queries are intended for educational purposes within this SOC laboratory.
