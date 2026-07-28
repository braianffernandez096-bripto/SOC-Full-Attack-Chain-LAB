# 🌐 Wireshark Evidence

## 📌 Overview

This directory contains the network captures collected during the simulated attack investigation.

The packet captures complement the endpoint telemetry gathered by Elastic SIEM and provide network-level visibility into attacker activity.

---

## 📁 Capture Contents

The captures included in this directory document the following activities:

| Scenario | Network Evidence |
|----------|------------------|
| Lateral Movement | SMB traffic over TCP/445 |
| Remote Administration | SMB session establishment |
| Authentication Activity | SMB authentication attempts |

---

## 🔍 Investigation Objectives

The network captures were analyzed to:

- Validate SMB communications observed in Elastic SIEM.
- Confirm remote administration activity.
- Correlate endpoint events with network traffic.
- Support reconstruction of the attack timeline.

---

## 📡 Evidence Sources

Network captures were collected using:

- Wireshark
- SMB Protocol
- TCP Port 445

---

## 🔗 Correlation

The packet captures should be analyzed together with:

- Windows Security Events
- Sysmon Network Events (Event ID 3)
- Elastic SIEM detections

Combining endpoint telemetry with packet-level evidence improves confidence during incident investigation.

---

## 🔒 Data Handling

Sensitive information has been partially sanitized.

The following information may be obfuscated:

- Internal IP addresses
- Hostnames
- Usernames

This sanitization does not affect the technical validity of the investigation.

- Internal IP addresses
- Hostnames
- Usernames

The applied sanitization does not affect the integrity of the investigation or the documented detection logic.
