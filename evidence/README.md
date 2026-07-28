Ahora veamos el README.md de wireshark:

📊 Evidence Overview

This directory contains the evidence collected throughout the simulated attack investigation.

The artifacts are organized according to the attack lifecycle, making it easier to correlate endpoint telemetry, authentication events, and network activity documented in the incident report.
📁 Evidence Structure
🟣 Elastic SIEM (Kibana)

Evidence is organized by attack phase.
Folder 	Description
01-brute-force 	Multiple failed authentication attempts (Event ID 4625)
02-initial-access 	Successful network logon (Event ID 4624)
03-privilege-escalation 	Administrative privileges assigned (Event ID 4672)
04-persistence 	Local account creation and administrator group membership (Event IDs 4720 / 4732)
05-lateral-movement 	SMB-related activity and remote access evidence
06-remote-execution 	Service creation and process execution (Event IDs 7045 / 4688)

These screenshots illustrate how each stage of the attack was identified and correlated within Elastic SIEM.
🔵 Wireshark

Network captures collected during the investigation.

Evidence includes:

    SMB communications (TCP/445)
    Authentication traffic
    Remote administration activity

These captures validate network behavior observed in the SIEM.
🟡 Endpoint Telemetry

Host-based telemetry collected from Sysmon and Windows Security Logs.

Evidence includes:

    Authentication events
    Process execution
    Service creation
    Account creation
    Privilege assignment

This telemetry provides visibility into attacker activity on the compromised endpoint.
🔄 Investigation Workflow

The incident was reconstructed by correlating evidence from multiple telemetry sources.

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
Incident Reconstruction

🔒 Data Handling

To protect sensitive information, selected screenshots have been sanitized.

The following information may be partially obfuscated:

    Internal IP addresses
    Hostnames
    Usernames

The applied sanitization does not affect the integrity of the investigation or the documented detection logic.

Está bien?
