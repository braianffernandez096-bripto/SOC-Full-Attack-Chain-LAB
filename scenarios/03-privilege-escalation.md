# 🟡 Privilege Escalation

## 📌 Objective

Simulate the use of elevated privileges following successful authentication and validate the detection of privileged sessions through Windows Security Events.

---

## 🧠 Attack Description

After successfully authenticating to the target system, the attacker gained access to a privileged account.

Windows generated a Special Logon event (Event ID 4672), indicating that the authenticated session was granted administrative privileges.

This event represents a significant increase in the attacker's capabilities, enabling actions such as persistence, remote execution, and lateral movement.

---

## 🔍 Detection

### Detection Query

```kql
event.code:4672
```

### Evidence

- Special Logon event (Event ID 4672)
- Administrative privileges assigned
- Privileged user session established

---

## 📊 Indicators of Compromise (IOC)

- Privileged logon session
- Administrative privileges assigned
- Elevated user context
- Authentication sequence consistent with privileged access

---

## 🧩 MITRE ATT&CK Mapping

| Tactic | Technique | MITRE ID |
|--------|-----------|-----------|
| **Defense Evasion / Persistence / Privilege Context** | Valid Accounts | **T1078** |

> **Note:** Event ID 4672 indicates that a session received special privileges. In this laboratory, it is correlated with the previous successful authentication (Event ID 4624) to demonstrate the attacker's transition to a privileged context.

---

## 📡 Evidence Sources

| Source | Evidence |
|--------|----------|
| **Windows Security Logs** | Event ID 4672 (Special Logon) |
| **Elastic SIEM** | Detection of privileged logon events |
| **Kibana** | Correlation of authentication and privilege assignment |

---

## 🚨 Analyst Assessment

The Special Logon event confirms that the authenticated account received elevated privileges within the operating system.

Although Event ID 4672 alone does not indicate malicious activity, its correlation with the successful authentication event and the subsequent attack stages provides strong evidence that the attacker operated with administrative privileges.

---

## 💡 Lessons Learned

- Privileged logon events should always be investigated within the context of the complete authentication sequence.
- Correlating Event IDs 4624 and 4672 helps identify potentially compromised privileged accounts.
- Monitoring administrative sessions provides early visibility into attacker activity before persistence or lateral movement occurs.
