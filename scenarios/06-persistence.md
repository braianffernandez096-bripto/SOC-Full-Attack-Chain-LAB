# 🟣 Persistence

## 📌 Objective

Simulate persistence by creating a new local user account and adding it to the local Administrators group, validating the detection of unauthorized account creation and privileged group membership.

---

## 🧠 Attack Description

After obtaining administrative privileges, the attacker established persistence by creating a new local user account and assigning it administrative permissions.

This technique allows continued access to the compromised system even if the original credentials are revoked or the initial attack vector is remediated.

---

## 🔍 Detection

### Detection Query

```kql
event.code:(4720 OR 4732)
```

### Evidence

- New local user account created (Event ID 4720)
- User added to the local Administrators group (Event ID 4732)

---

## 📊 Indicators of Compromise (IOC)

- Unauthorized local account creation
- User added to the Administrators group
- Newly created privileged account
- Administrative account not following normal provisioning procedures

---

## 🧩 MITRE ATT&CK Mapping

| Tactic | Technique | MITRE ID |
|--------|-----------|-----------|
| **Persistence** | Create Account | **T1136** |

---

## 📡 Evidence Sources

| Source | Evidence |
|--------|----------|
| **Windows Security Logs** | Event IDs 4720 and 4732 |
| **Elastic SIEM** | Detection of account creation and group membership events |
| **Kibana** | Correlation of persistence-related activity |

---

## 🚨 Analyst Assessment

The creation of a new privileged local account indicates an attempt to establish long-term access to the compromised endpoint.

Although administrative account creation can be legitimate in enterprise environments, unexpected account creation followed by immediate assignment to the Administrators group should be considered highly suspicious, particularly when correlated with previous authentication, privilege escalation, and lateral movement events.

---

## 💡 Lessons Learned

- Monitoring local account creation is essential for detecting persistence mechanisms.
- Administrative group membership changes should be closely monitored and validated.
- Correlating account creation with previous attack stages significantly improves investigation accuracy.
- Persistence techniques often appear after attackers have obtained privileged access, making event correlation critical during incident response.
