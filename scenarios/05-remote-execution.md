🔵 Remote Execution
📌 Description

The attacker executed commands remotely on the target system using service-based techniques.

🧠 Behavior Observed
Service creation
Process execution under SYSTEM

🔍 Detection
event.code:7045 OR event.code:4688

📊 Indicators
New service installed
Suspicious process execution
SYSTEM-level execution

🧩 MITRE ATT&CK
T1059 — Command Execution

🚨 Analyst Note

This stage confirms active control over the system.
