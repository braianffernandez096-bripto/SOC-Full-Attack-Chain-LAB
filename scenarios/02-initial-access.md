🟠 Initial Access

📌 Description

Following the brute force attack, a successful authentication was observed, indicating that valid credentials were obtained.

🧠 Behavior Observed
Successful login after multiple failures
Network-based authentication

🔍 Detection
event.code:4624 AND winlog.event_data.LogonType:3

📊 Indicators
Login success after multiple failures
External source access
Network logon

🧩 MITRE ATT&CK
T1078 — Valid Accounts

🚨 Analyst Note

This stage confirms that the attacker successfully gained access using valid credentials.
