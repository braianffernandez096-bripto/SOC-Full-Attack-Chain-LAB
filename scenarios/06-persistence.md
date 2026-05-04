🟣 Persistence
📌 Description

The attacker established persistence by creating a new user and adding it to the administrators group.

🧠 Behavior Observed
New user creation
Privileged group assignment

🔍 Detection
event.code:4720 OR event.code:4732

📊 Indicators
Unauthorized account creation
Privilege escalation via groups

🧩 MITRE ATT&CK
T1136 — Create Account

🚨 Analyst Note

Persistence ensures continued access even if the original entry point is closed.
