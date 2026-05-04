🔵 Lateral Movement
📌 Description

The attacker attempted to move laterally within the network using SMB protocol.

🧠 Behavior Observed
SMB traffic (port 445)
Access attempts to administrative shares (IPC$, C$)

🔍 Detection
destination.port:445

📊 Indicators
Access to network shares
Repeated SMB connections

🧩 MITRE ATT&CK
T1021 — Remote Services (SMB)

🚨 Analyst Note

Even failed access attempts are valuable indicators of lateral movement attempts.
