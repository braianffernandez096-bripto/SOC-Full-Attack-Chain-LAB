🔴 Brute Force Attack
📌 Description

This stage simulates a brute force attack against a Windows endpoint, where multiple failed authentication attempts are performed in a short period of time.

🧠 Behavior Observed
High number of failed login attempts
Repeated authentication requests from the same source
Rapid succession of login failures

🔍 Detection
event.code:4625

📊 Indicators
Multiple failed logons
Same username targeted
High frequency in short timeframe

🧩 MITRE ATT&CK
T1110 — Brute Force

🚨 Analyst Note

A single failed login is normal, but a high volume in a short period is a strong indicator of automated attack activity.
