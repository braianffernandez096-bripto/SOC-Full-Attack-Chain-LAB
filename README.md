# SOC-Full-Attack-Chain-LAB
Full Attack Chain Lab for SOC

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Platform](https://img.shields.io/badge/Platform-Windows%2010-blue)
![SIEM](https://img.shields.io/badge/SIEM-Elastic%20Stack-purple)
![Sysmon](https://img.shields.io/badge/Telemetry-Sysmon-blue)
![Winlogbeat](https://img.shields.io/badge/Log%20Forwarder-Winlogbeat-orange)
![KQL](https://img.shields.io/badge/Detection-KQL-blue)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-Mapped-red)
![Wireshark](https://img.shields.io/badge/Network%20Analysis-Wireshark-blue)

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

---

## 🚨 Impact Assessment

The investigation confirmed that the simulated attacker successfully progressed through multiple stages of the attack lifecycle, resulting in a complete compromise of the target endpoint.

The following activities were observed during the investigation:

| Impact | Evidence |
|--------|----------|
| **Unauthorized Access** | Successful authentication after multiple failed logon attempts (Event ID 4624) |
| **Privilege Escalation** | Administrative privileges assigned (Event ID 4672) |
| **Persistence** | Local administrator account created and added to the Administrators group (Event IDs 4720 / 4732) |
| **Lateral Movement** | SMB communications and remote execution activity |
| **Command Execution** | Process creation events and service execution (Event ID 4688 / 7045) |

### Security Assessment

The attack demonstrates how an adversary can transition from initial access to full endpoint compromise by chaining together multiple techniques.

The investigation also highlights the value of correlating endpoint telemetry, authentication events, and network evidence to accurately reconstruct attacker activity throughout the incident.

---

## 💡 Lessons Learned

This project reinforced the importance of analyzing security incidents through the correlation of multiple telemetry sources rather than relying on isolated events.

Some of the key takeaways from this laboratory include:

- Correlating Windows Security Events with Sysmon telemetry provides greater visibility into attacker activity.
- Network evidence collected with Wireshark complements endpoint telemetry and helps validate attacker behavior.
- Mapping observed activity to the MITRE ATT&CK framework improves incident documentation and communication.
- Building a structured attack timeline simplifies incident investigation and supports faster decision-making during analysis.

Overall, this lab strengthened practical skills in threat detection, event correlation, and incident investigation within a SOC environment.

---

## 📄 Documentation

Additional technical documentation for this project is available in the `docs/` directory.

- **Full Incident Report** – Complete investigation, evidence correlation, impact assessment, and recommendations.
- **Detection Queries** – KQL queries used during the investigation.
- **Attack Scenario** – Detailed description of the simulated attack chain.
