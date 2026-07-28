# 🔴 Brute Force Attack

## 📌 Objective

Simulate a brute-force attack against a Windows endpoint to generate multiple failed authentication attempts and validate the ability of the SIEM to detect and correlate suspicious login activity.

---

## 🧠 Attack Description

The attacker repeatedly attempted to authenticate to a Windows account using invalid credentials within a short period of time.

This activity generated multiple failed logon events, providing a clear indicator of automated password guessing behavior.

---

## 🔍 Detection

### Detection Query

```kql
event.code:4625
```

### Evidence

- Multiple failed authentication attempts
- Repeated logons targeting the same user account
- High authentication frequency over a short time interval

---

## 📊 Indicators of Compromise (IOC)

- High volume of failed logon attempts
- Repeated authentication failures against the same account
- Authentication events occurring within a short timeframe

---

## 🧩 MITRE ATT&CK Mapping

| Tactic | Technique | MITRE ID |
|--------|-----------|-----------|
| **Credential Access** | Brute Force | **T1110** |

---

## 📡 Evidence Sources

| Source | Evidence |
|--------|----------|
| **Windows Security Logs** | Event ID 4625 |
| **Elastic SIEM** | Authentication event correlation |
| **Kibana** | Timeline visualization of failed logons |

---

## 🚨 Analyst Assessment

While isolated failed authentication attempts are common in enterprise environments, a sustained sequence of failed logons targeting the same account within a short period is a strong indicator of brute-force activity.

In this laboratory, the generated events were successfully identified and correlated through Elastic SIEM, demonstrating visibility into the initial stage of the attack.

---

## 💡 Lessons Learned

- Failed authentication events provide valuable indicators for detecting password attacks.
- Correlating authentication attempts over time significantly improves detection accuracy.
- Proper account lockout policies help mitigate brute-force attacks before successful compromise.
