# 🛡️ Incident Report — Full Attack Chain Analysis

## 📌 Executive Summary

This report documents the investigation of a simulated multi-stage cyber attack against a Windows 10 endpoint within a controlled SOC laboratory.

The objective of the investigation was to reconstruct the complete attack lifecycle by correlating endpoint telemetry, Windows Security Events, and network evidence collected through Elastic Stack, Sysmon, Winlogbeat, and Wireshark.

The attack consisted of brute force authentication attempts, successful network authentication, privilege escalation, persistence, lateral movement through SMB, and remote command execution.

---

## 🎯 Incident Overview

| Category | Details |
|----------|---------|
| **Incident Type** | Multi-Stage Attack Simulation |
| **Environment** | Windows 10 • Kali Linux • Ubuntu (Elastic Stack) |
| **Detection Platform** | Elastic Stack (Elasticsearch & Kibana) |
| **Endpoint Telemetry** | Sysmon + Windows Security Logs |
| **Log Collection** | Winlogbeat |
| **Network Analysis** | Wireshark |
| **Framework** | MITRE ATT&CK |

---

## 🧠 Attack Narrative

The attacker initiated a brute-force attack against a Windows user account, generating multiple failed authentication attempts.

After obtaining valid credentials, a successful network logon was observed, allowing access to the target endpoint.

Administrative privileges were subsequently assigned, enabling actions beyond the permissions of a standard user.

The attacker established persistence by creating a new local account and adding it to the local Administrators group.

Using SMB administrative shares, remote execution was performed through service creation, resulting in command execution on the compromised endpoint.

The investigation reconstructed every stage of the intrusion by correlating authentication logs, endpoint telemetry, and network traffic.

---

## 🕒 Attack Timeline

| Attack Phase | Evidence | Description |
|--------------|----------|-------------|
| **Brute Force** | Event ID **4625** | Multiple failed authentication attempts |
| **Initial Access** | Event ID **4624** | Successful network logon (Logon Type 3) |
| **Privilege Escalation** | Event ID **4672** | Administrative privileges assigned |
| **Persistence** | Event IDs **4720 / 4732** | Local user creation and administrator group membership |
| **Lateral Movement** | SMB (TCP/445) | Communication through administrative shares |
| **Remote Execution** | Event IDs **7045 / 4688** | Service creation and process execution |

---

## 📊 Investigation Summary

| Investigation Area | Result |
|--------------------|--------|
| Brute Force Detection | ✅ Confirmed |
| Successful Authentication | ✅ Confirmed |
| Privilege Escalation | ✅ Confirmed |
| Persistence | ✅ Confirmed |
| Lateral Movement | ✅ Confirmed |
| Remote Execution | ✅ Confirmed |
| Multi-source Correlation | ✅ Successful |

---

## 📡 Evidence Correlation

The investigation combined multiple telemetry sources to validate attacker activity throughout the attack lifecycle.

| Source | Evidence Collected |
|--------|--------------------|
| **Elastic SIEM** | Authentication events, privilege escalation, process execution and event correlation |
| **Windows Security Logs** | Failed logons, successful authentication, privileged logons, account creation |
| **Sysmon** | Process creation and endpoint activity |
| **Wireshark** | SMB communications and network validation |

The combination of endpoint telemetry and network evidence enabled a complete reconstruction of the incident.

---

## 🔍 Detection Logic

The following detection queries were used during the investigation.

| Detection Query | Purpose |
|-----------------|---------|
| `event.code:4625` | Detect brute-force authentication attempts |
| `event.code:4624 AND winlog.event_data.LogonType:3` | Identify successful network logons |
| `event.code:4672` | Detect privileged logons |
| `event.code:4720 OR event.code:4732` | Detect persistence through account creation |
| `event.code:7045 OR event.code:4688` | Identify remote execution through service and process creation |

---

## 🧩 MITRE ATT&CK Mapping

The observed attacker behavior was mapped to the MITRE ATT&CK framework.

| Tactic | Technique | MITRE ID | Evidence |
|--------|-----------|----------|----------|
| **Credential Access** | Brute Force | **T1110** | Multiple failed authentication attempts (Event ID 4625) |
| **Initial Access** | Valid Accounts | **T1078** | Successful authentication (Event ID 4624) |
| **Persistence** | Create Account | **T1136** | Local administrator account creation (Event ID 4720) |
| **Lateral Movement** | SMB / Windows Admin Shares | **T1021.002** | SMB communication (TCP/445) |
| **Execution** | Command and Scripting Interpreter | **T1059** | Remote command execution (Event ID 4688 / 7045) |

---

## 🚨 Impact Assessment

The investigation confirmed that the simulated attacker successfully progressed through multiple stages of the attack lifecycle, resulting in a complete compromise of the target endpoint.

| Impact | Evidence |
|--------|----------|
| **Unauthorized Access** | Successful authentication following multiple failed logons |
| **Privilege Escalation** | Administrative privileges assigned (Event ID 4672) |
| **Persistence** | Local administrator account creation |
| **Lateral Movement** | SMB administrative share activity |
| **Command Execution** | Service creation and process execution |

The correlation of authentication events, endpoint telemetry, and network traffic provided high confidence in the reconstruction of the attack.

---

## 🚨 Incident Severity

| Severity | Assessment |
|----------|------------|
| **High** | Confirmed unauthorized access, privilege escalation, persistence, lateral movement, and remote command execution within the target endpoint. |

---

## 💡 Lessons Learned

This investigation reinforced the importance of correlating multiple telemetry sources rather than relying on isolated events.

Key observations include:

- Windows Security Events provide visibility into authentication and privilege-related activity.
- Sysmon significantly improves endpoint visibility by recording process execution.
- Network traffic captured with Wireshark complements endpoint telemetry and validates attacker behavior.
- Mapping observed activity to the MITRE ATT&CK framework improves incident documentation and analyst communication.
- Building a structured attack timeline simplifies incident reconstruction and supports faster analysis.

---

## 🔐 Recommendations

| Recommendation | Objective |
|---------------|-----------|
| Implement account lockout policies | Reduce brute-force attacks |
| Monitor privileged logons (Event ID 4672) | Detect privilege escalation |
| Restrict SMB administrative shares | Reduce lateral movement opportunities |
| Monitor service creation events (Event ID 7045) | Detect remote execution |
| Apply the Principle of Least Privilege | Limit attacker capabilities |
| Improve SIEM correlation rules | Increase detection coverage and reduce response time |

---

## 📌 Final Assessment

The simulated incident demonstrates how a complete attack chain can be reconstructed through the correlation of endpoint telemetry, authentication events, and network evidence.

Rather than relying on individual alerts, the investigation combined multiple data sources to achieve a comprehensive understanding of attacker behavior.

This project reflects a practical SOC investigation workflow and demonstrates techniques commonly used by Security Operations Center analysts during incident response and threat investigation.
