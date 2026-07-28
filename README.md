# SOC-Full-Attack-Chain-LAB
Full Attack Chain Lab for SOC

A SOC lab simulating a full attack chain (detection via Elastic Stack: brute force, lateral movement, remote execution), featuring:

🛡️ Full Attack Chain Lab for SOC — End-to-End Detection

📌 Overview

This project simulates a complete cyber attack chain from the perspective of a Security Operations Center (SOC), focusing on threat detection, event correlation, and incident investigation using the Elastic Stack.


---

## 🏗️ Lab Architecture

The lab was designed to simulate a realistic enterprise environment where endpoint telemetry and network traffic can be collected, centralized, and analyzed through a SIEM.

```text
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

### Environment

| Machine | Role | Main Components |
|----------|------|-----------------|
| **Kali Linux** | Attacker | Attack simulations (SMB, PowerShell, HTTP) |
| **Windows 10** | Victim Endpoint | Sysmon, Winlogbeat, Windows Security Logs |
| **Ubuntu Server** | SIEM Platform | Elasticsearch, Kibana |

### Data Flow

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

## 🧠 Scenario

The objective of this lab was to simulate a realistic attack against a Windows endpoint and reconstruct each stage of the intrusion using endpoint telemetry and network evidence.

The investigation focused on correlating Windows Security Events, Sysmon telemetry, Elastic SIEM detections, and Wireshark packet captures to identify attacker activity throughout the entire attack lifecycle.


## 🕒 Attack Timeline

The following timeline summarizes the attack progression observed during the investigation.

```text
Brute Force
      │
      ▼
Successful Authentication
      │
      ▼
Privilege Escalation
      │
      ▼
Persistence
      │
      ▼
Lateral Movement (SMB)
      │
      ▼
Remote Execution

```

| Attack Phase | Evidence |
|--------------|----------|
| **Brute Force** | Windows Security Event ID 4625 |
| **Successful Authentication** | Windows Security Event ID 4624 |
| **Privilege Escalation** | Windows Security Event ID 4672 |
| **Persistence** | Windows Security Event IDs 4720 / 4732 |
| **Lateral Movement** | SMB Traffic (TCP/445) |
| **Remote Execution** | Event ID 4688 / 7045 |
| **Command & Control** | Sysmon Event ID 3 + Wireshark |

---

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
