# SOC-Full-Attack-Chain-LAB
Full Attack Chain Lab for SOC

A SOC lab simulating a full attack chain (detection via Elastic Stack: brute force, lateral movement, remote execution), featuring:

🛡️ Full Attack Chain Lab for SOC — End-to-End Detection

📌 Overview

This project simulates a full attack chain from the perspective of a SOC (Security Operations Center), focusing on the detection and analysis of attacker behavior.

The lab was built using Elastic Stack (SIEM), Sysmon, and Winlogbeat, with a Windows 10 endpoint (client machine) and Kali Linux as the attacker machine.


🏗️ Lab Architecture

The lab was designed to simulate a realistic enterprise environment where endpoint telemetry and network traffic can be collected, centralized, and analyzed through a SIEM.

                 Kali Linux
                      │
      SMB / PowerShell / HTTP Simulations
                      │
                      ▼
+-----------------------------------------------+
| Windows 10 Victim                             |
| • Sysmon                                      |
| • Winlogbeat                                  |
| • Windows Security Logs                       |
+-----------------------------------------------+
                      │
               Log Collection
                      │
                      ▼
+-----------------------------------------------+
| Ubuntu Server                                 |
| • Elasticsearch                               |
| • Kibana                                      |
| • Elastic Stack                               |
+-----------------------------------------------+
```

Environment

| Machine | Role | Main Components |
|----------|------|-----------------|
| **Kali Linux** | Attacker | Attack simulations (SMB, PowerShell, HTTP) |
| **Windows 10** | Victim Endpoint | Sysmon, Winlogbeat, Windows Security Logs |
| **Ubuntu Server** | SIEM Platform | Elasticsearch, Kibana |

Data Flow

```
Attack Simulation
        │
        ▼
Windows Endpoint
        │
Sysmon + Windows Security Logs
        │
Winlogbeat
        │
Elasticsearch
        │
Kibana
        │
Detection & Investigation
```

🧠 Scenario

The attack begins with a brute-force attempt against a Windows system, followed by successful authentication, privilege escalation, lateral movement via SMB, and remote execution.

The objective is to detect and correlate each stage using the SIEM and network analysis. 🔴 Attack stages

Brute force (Event ID 4625)

Successful login (Event ID 4624)

Privilege escalation (Event ID 4672)

User creation and persistence (Event ID 4720 / 4732)

Lateral movement via SMB (Port 445)

Remote execution (Event ID 7045 / 4688)

📡 Detection approach

Detection was performed using:

Elastic SIEM (log correlation)

Sysmon (endpoint telemetry)

Wireshark (network analysis)

🧩 MITRE ATT&CK

T1110 — Brute Force

T1078 — Valid Accounts

T1021 — Remote Services

T1059 — Command Execution

T1136 — Account Creation

🚨 Impact

The attacker achieved:

Unauthorized access

Privilege escalation

Lateral movement

Remote code execution

👉 Full endpoint compromise.

💡 Conclusion:
This lab demonstrates how a full attack chain can be reconstructed by correlating events from multiple data sources.
