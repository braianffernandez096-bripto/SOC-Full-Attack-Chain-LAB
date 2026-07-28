# 🔵 Remote Execution

## 📌 Objective

Simulate remote command execution through Windows service creation and validate the detection of service installation and process execution using Elastic SIEM.

---

## 🧠 Attack Description

After achieving privileged access and lateral movement, the attacker remotely executed commands on the target endpoint by creating a Windows service.

The execution generated Windows events indicating both service installation and process creation, confirming that code was executed with elevated privileges.

This stage represents full operational control of the compromised endpoint.

---

## 🔍 Detection

### Detection Query

```kql
event.code:(7045 OR 4688)
```

### Evidence

- Windows service creation (Event ID 7045)
- Process execution (Event ID 4688)
- Execution under a privileged security context

---

## 📊 Indicators of Compromise (IOC)

- New Windows service installed
- Unexpected process execution
- Execution under SYSTEM or administrative privileges
- Service creation outside normal administrative activity

---

## 🧩 MITRE ATT&CK Mapping

| Tactic | Technique | MITRE ID |
|--------|-----------|-----------|
| **Execution** | Service Execution | **T1569.002** |

> **Note:** Event ID 7045 confirms the creation of a Windows service. Event ID 4688 complements the investigation by providing visibility into the executed process.

---

## 📡 Evidence Sources

| Source | Evidence |
|--------|----------|
| **Windows Security Logs** | Event ID 7045 (Service Creation) |
| **Sysmon / Windows Logs** | Event ID 4688 (Process Creation) |
| **Elastic SIEM** | Correlation of service creation and process execution |
| **Kibana** | Timeline of remote execution events |

---

## 🚨 Analyst Assessment

The creation of a new Windows service followed by process execution confirms that the attacker successfully executed code on the compromised endpoint.

Although service creation can occur during legitimate software installation or system administration, unexpected service creation following privilege escalation and lateral movement should be considered highly suspicious.

Correlating these events with previous stages of the attack provides high confidence that the endpoint was fully compromised.

---

## 💡 Lessons Learned

- Windows service creation is a high-value indicator for detecting remote execution.
- Process creation events provide additional context for understanding attacker activity.
- Correlating service creation with authentication and privilege-related events significantly improves investigation accuracy.
- Multi-source telemetry enables analysts to reconstruct remote execution with high confidence.
