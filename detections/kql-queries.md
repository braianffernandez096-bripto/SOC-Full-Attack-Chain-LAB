🔍 Detection Queries — SOC Lab

This section contains detection logic used to identify each stage of the attack chain using Kibana Query Language (KQL).

🔴 Brute Force Detection

Detect multiple failed login attempts:

event.code: 4625

High frequency of these events in a short period may indicate a brute force attack.

🟠 Successful Login After Brute Force
event.code:4624 AND winlog.event_data.LogonType: 3

Indicates successful authentication over the network, potentially after password guessing.

🟡 Privilege Escalation
event.code:4672

Special privileges assigned to a new logon session.

🟡 User Creation (Persistence)
event.code:4720

A new account was created on the system.

🟡 Add User to Administrators Group
event.code:4732

User added to a privileged group.

🔵 Lateral Movement (SMB Activity)
destination.port:445

SMB traffic that may indicate lateral movement or remote access attempts.

🔵 Remote Execution — Service Creation
event.code:7045

A service was installed on the system (common in remote execution techniques like PsExec).

🔵 Remote Execution — Process Creation
event.code:4688

New process execution, useful for identifying suspicious binaries.

🧠 Correlation Tip

A high-confidence detection can be achieved by correlating:

Multiple 4625 events
Followed by a 4624 success
Followed by 4672 (privileges)
Followed by 7045 or 4688 (execution)

(event.code:4625 OR event.code:4624 OR event.code:4672 OR event.code:7045)

👉 This sequence strongly indicates a full attack chain.
