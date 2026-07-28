# 🔵 Lateral Movement

## 📌 Objective

Simulate lateral movement through SMB administrative shares and validate the detection of remote access attempts using endpoint telemetry and network evidence.

---

## 🧠 Attack Description

Following successful authentication and privileged access, the attacker attempted to move laterally within the environment by interacting with SMB administrative shares.

Network activity over TCP port 445 and access attempts to administrative shares such as **IPC$** and **C$** were observed during the investigation.

---

## 🔍 Detection

### Detection Query

```kql
destination.port:445
```

> *If your Sysmon logs support it, you can replace it with:*

```kql
event.code:3 AND destination.port:445
```

### Evidence

- SMB communications over TCP/445
- Access attempts to administrative shares
- Network connections associated with remote administration

---

## 📊 Indicators of Compromise (IOC)

- SMB traffic over TCP/445
- Access to administrative shares (IPC$, C$)
- Repeated SMB connections
- Remote administrative activity

---

## 🧩 MITRE ATT&CK Mapping

| Tactic | Technique | MITRE ID |
|--------|-----------|-----------|
| **Lateral Movement** | SMB/Windows Admin Shares | **T1021.002** |

---

## 📡 Evidence Sources

| Source | Evidence |
|--------|----------|
| **Sysmon** | Network connection events (Event ID 3) |
| **Elastic SIEM** | Correlation of SMB-related activity |
| **Wireshark** | SMB traffic over TCP/445 |
| **Kibana** | Timeline of network activity |

---

## 🚨 Analyst Assessment

The observed SMB communications indicate an attempt to interact with remote administrative shares after privileged access was obtained.

Although access attempts may not always succeed, this type of activity is a valuable indicator of potential lateral movement and should be investigated in the context of preceding authentication and privilege-related events.

The correlation between authentication events, privileged sessions, endpoint telemetry, and network traffic strengthens confidence in the reconstruction of this attack stage.

---

## 💡 Lessons Learned

- SMB traffic should be monitored for signs of unauthorized remote administration.
- Network evidence complements endpoint telemetry when investigating lateral movement.
- Administrative share access is common in enterprise environments but should be validated against user behavior and authentication history.
- Correlating SMB activity with previous attack stages improves the accuracy of incident investigations.
