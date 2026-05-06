🛡️ Incident Report — Full Attack Chain Analysis

📌 Executive Summary

A security incident was identified involving a complete attack chain against a Windows 10 endpoint.
The attack started with a brute force attempt, followed by successful authentication, privilege escalation, lateral movement via SMB, and culminated in remote code execution and persistence.

The analysis was conducted using Elastic SIEM, Sysmon telemetry, and network traffic inspection via Wireshark.

🧠 Attack Narrative

The attacker initiated a brute force attack targeting a user account, generating multiple failed authentication attempts.

After successfully obtaining valid credentials, the attacker gained access to the system via network logon.

Once inside, elevated privileges were assigned, allowing further actions. The attacker then attempted lateral movement using SMB protocol and administrative shares.

Subsequently, remote execution was performed through service creation, enabling command execution under SYSTEM privileges.

Finally, persistence was established by creating a new user account and adding it to the administrators group.

🕒 Attack Timeline
Stage	Event	Description
Brute Force	4625	Multiple failed logons
Initial Access	4624	Successful login (Logon Type 3)
Privilege Escalation	4672	Admin privileges assigned
Persistence	4720 / 4732	User creation + admin group
Lateral Movement	SMB (445)	Access to IPC$ / C$
Remote Execution	7045 / 4688	Service + process execution

📡 Evidence Correlation

The incident was validated through multiple data sources:

SIEM (Kibana): authentication events, privilege escalation, process execution
Network (Wireshark): SMB traffic and authentication attempts
Endpoint: service creation and process activity

This multi-layer correlation confirms attacker activity across the environment.

🔍 Detection Logic
event.code:4625
event.code:4624 AND winlog.event_data.LogonType:3
event.code:4672
event.code:4720 OR event.code:4732
event.code:7045 OR event.code:4688

🧩 MITRE ATT&CK Mapping
T1110 — Brute Force
T1078 — Valid Accounts
T1021 — Remote Services (SMB)
T1059 — Command Execution
T1136 — Create Account

🚨 Impact Assessment

The attacker successfully achieved:

Unauthorized access
Privilege escalation
Lateral movement
Remote code execution
Persistence within the system

👉 This represents a full compromise of the endpoint.

🚨 Incident Severity

High

Due to confirmed remote execution and persistence mechanisms, the incident represents a critical security breach.

💡 Conclusion

This case demonstrates how a full attack chain can be reconstructed through proper log correlation and multi-source analysis.

The visibility provided by SIEM, endpoint telemetry and network monitoring was essential to identify each stage of the attack.

🔐 Recommendations
Implement account lockout policies to mitigate brute force attacks
Monitor privilege escalation events (Event ID 4672)
Restrict SMB access and administrative shares
Monitor service creation events (Event ID 7045)
Apply least privilege principle
Enhance alerting rules in SIEM
