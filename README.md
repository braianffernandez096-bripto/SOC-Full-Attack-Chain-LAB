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

## 🔍 Detection Logic

Rather than relying on a single alert, the investigation focused on correlating multiple telemetry sources to reconstruct the attack chain.

The following data sources were analyzed throughout the investigation:

| Data Source | Purpose |
|-------------|---------|
| Windows Security Logs | Authentication events, privilege escalation, account creation |
| Sysmon | Process creation and network connections |
| Elastic SIEM | Event correlation and timeline reconstruction |
| Wireshark | Network traffic validation and protocol analysis |

### Detection Workflow

1. Multiple failed authentication attempts were identified through Windows Security Event ID **4625**.

2. A successful logon (Event ID **4624**) from the same user indicated that valid credentials had been obtained.

3. Administrative privileges were confirmed using Event ID **4672**, suggesting privilege escalation.

4. Account creation events (**4720**) and group membership changes (**4732**) revealed persistence mechanisms.

5. Process creation and network activity collected by Sysmon were correlated with SMB traffic captured in Wireshark to validate remote execution and attacker movement.

This correlation allowed the complete attack chain to be reconstructed with a high level of confidence.

### Investigation Flow

```text
Windows Security Logs
          │
          ▼
       Sysmon
          │
          ▼
     Elastic SIEM
          │
          ▼
     Wireshark
          │
          ▼
Attack Reconstruction

```

---

---

## 🧩 MITRE ATT&CK Mapping

The simulated attack was mapped to the MITRE ATT&CK framework to classify the adversary's tactics and techniques observed throughout the investigation.

| Tactic | Technique | MITRE ID | Evidence |
|--------|-----------|----------|----------|
| **Credential Access** | Brute Force | **T1110** | Multiple failed authentication attempts (Event ID 4625) |
| **Initial Access** | Valid Accounts | **T1078** | Successful authentication (Event ID 4624) |
| **Persistence** | Create Account | **T1136** | Local administrator account created (Event ID 4720) |
| **Lateral Movement** | Remote Services (SMB) | **T1021.002** | SMB traffic (TCP/445) and remote execution |
| **Execution** | Command and Scripting Interpreter | **T1059** | Remote process execution (Event ID 4688 / 7045) |

### MITRE Coverage

This laboratory demonstrates how multiple ATT&CK techniques can be identified by correlating endpoint telemetry, authentication events, and network traffic, providing greater visibility into the attack lifecycle.
---

## 📊 Skills Demonstrated

This project demonstrates practical experience across multiple areas of Security Operations (SOC), including endpoint monitoring, event correlation, threat detection, and incident investigation.

| Category | Skills Demonstrated |
|----------|---------------------|
| **SIEM** | Elastic Stack (Elasticsearch & Kibana) |
| **Endpoint Monitoring** | Sysmon |
| **Log Collection** | Winlogbeat |
| **Threat Detection** | Behavioral analysis and event correlation |
| **Incident Investigation** | Attack timeline reconstruction |
| **Network Analysis** | Wireshark packet analysis |
| **Authentication Analysis** | Windows Security Event investigation |
| **Frameworks** | MITRE ATT&CK Mapping |

### Core Competencies

- Security Monitoring
- Threat Detection
- Event Correlation
- Incident Investigation
- Endpoint Telemetry Analysis
- Network Traffic Analysis
- IOC Identification
- MITRE ATT&CK Mapping

🚨 Impact

The attacker achieved:

Unauthorized access

Privilege escalation

Lateral movement

Remote code execution

👉 Full endpoint compromise.

💡 Conclusion:
This lab demonstrates how a full attack chain can be reconstructed by correlating events from multiple data sources.
