# SOC-Full-Attack-Chain-LAB
SOC lab simulando una Cadena de Ataque Completa ( detección usando Elastic Stack.brute force, lateral movement, remote execution) con

🛡️ SOC Full Attack Chain Lab — End-to-End Detection

📌 Overview

This project simulates a full attack chain from a SOC (Security Operations Center) perspective, focusing on detection and analysis of attacker behavior.

The lab was built using Elastic Stack (SIEM), Sysmon and Winlogbeat, with a Windows 10 endpoint and Kali Linux as the attacker machine.

🧠 Scenario

The attack begins with a brute force attempt against a Windows system, followed by successful authentication, privilege escalation, lateral movement via SMB and remote execution.

The objective is to detect and correlate each stage using SIEM and network analysis.

🔴 Attack Stages

Brute Force (Event ID 4625)

Successful Login (Event ID 4624)

Privilege Escalation (Event ID 4672)

User Creation & Persistence (Event ID 4720 / 4732)

Lateral Movement via SMB (Port 445)

Remote Execution (Event ID 7045 / 4688)

📡 Detection Approach

Detection was performed using:

Elastic SIEM (log correlation)

Sysmon (endpoint telemetry)

Wireshark (network analysis)

🧩 MITRE ATT&CK

T1110 — Brute Force

T1078 — Valid Accounts

T1021 — Remote Services

T1059 — Command Execution

T1136 — Create Account

🚨 Impact

The attacker achieved:

Unauthorized access

Privilege escalation

Lateral movement

Remote code execution

👉 Full compromise of the endpoint.

💡 Conclusion

This lab demonstrates how a full attack chain can be reconstructed through event correlation across multiple data sources.
