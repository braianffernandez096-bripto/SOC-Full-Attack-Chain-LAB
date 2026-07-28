# 🟠 Initial Access

## 📌 Objective

Simulate successful authentication following a brute-force attack to validate the detection of compromised credentials and identify the transition from failed logon attempts to confirmed access.

---

## 🧠 Attack Description

After multiple failed authentication attempts, the attacker successfully authenticated to the target Windows endpoint using valid credentials.

The successful network logon confirmed that the brute-force attack resulted in unauthorized access to the system.

---

## 🔍 Detection

### Detection Query

```kql
event.code:4624 AND winlog.event_data.LogonType:3
```

### Evidence

- Successful network authentication
- Logon Type 3 (Network Logon)
- Authentication following repeated failed logon attempts

---

## 📊 Indicators of Compromise (IOC)

- Successful authentication after multiple failed attempts
- Network logon (Type 3)
- Access obtained using valid credentials
- Authentication sequence consistent with brute-force compromise

---

## 🧩 MITRE ATT&CK Mapping

| Tactic | Technique | MITRE ID |
|--------|-----------|-----------|
| **Initial Access** | Valid Accounts | **T1078** |

---

## 📡 Evidence Sources

| Source | Evidence |
|--------|----------|
| **Windows Security Logs** | Event ID 4624 (Successful Logon) |
| **Elastic SIEM** | Authentication event correlation |
| **Kibana** | Timeline showing successful authentication following failed logons |

---

## 🚨 Analyst Assessment

The successful network logon confirms that the attacker obtained valid credentials and gained unauthorized access to the target system.

When correlated with the preceding failed authentication attempts (Event ID 4625), this event represents the transition from a credential attack to a confirmed compromise.

---

## 💡 Lessons Learned

- Successful logon events should always be analyzed in the context of preceding authentication activity.
- Correlating Event IDs 4625 and 4624 significantly improves the detection of successful brute-force attacks.
- Monitoring network logons helps identify unauthorized remote access to Windows systems.
