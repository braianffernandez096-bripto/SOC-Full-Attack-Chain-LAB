# 📊 Evidence Overview

This directory contains the evidence collected during the simulated attack investigation.

The artifacts included in this repository support the findings documented in the incident report and demonstrate how multiple telemetry sources were correlated to reconstruct the complete attack chain.

---

## 📁 Evidence Categories

### 🟣 Elastic SIEM (Kibana)

Evidence collected from Elastic Stack used during the investigation.

Examples include:

- Brute force attempts (Event ID 4625)
- Successful authentication (Event ID 4624)
- Privileged logons (Event ID 4672)
- User creation (Event IDs 4720 / 4732)
- Process creation (Event ID 4688)
- Service creation (Event ID 7045)

These screenshots illustrate how authentication, privilege escalation, persistence, and command execution were identified through SIEM correlation.

---

### 🔵 Wireshark

Network traffic captured during the attack simulation.

Evidence includes:

- SMB communications (TCP/445)
- Authentication traffic
- Session establishment
- Remote administration activity

The captured traffic complements endpoint telemetry and validates attacker movement across the network.

---

### 🟡 Endpoint Telemetry

Host-based evidence collected through Sysmon and Windows Security Logs.

Examples include:

- Process execution
- Service installation
- Local account creation
- Privilege assignment
- Authentication events

This telemetry provides visibility into attacker actions performed directly on the compromised endpoint.

---

## 🔍 Investigation Workflow

The investigation was performed by correlating multiple telemetry sources rather than relying on individual events.

```text
Windows Security Logs
        │
        ▼
      Sysmon
        │
        ▼
 Elastic Stack (SIEM)
        │
        ▼
    Wireshark
        │
        ▼
Attack Reconstruction
```

---

## 🔒 Data Handling

To protect sensitive information, selected screenshots have been sanitized.

The following information may be partially obfuscated:

- Internal IP addresses
- Hostnames
- Usernames
- Domain names (if applicable)

This does not affect the integrity of the investigation or the detection logic presented throughout the project.
