# 🔍 KQL Detection Queries

## 📌 Overview

This document contains the KQL (Kibana Query Language) queries used throughout the investigation of the simulated full attack chain.

The detections are organized according to the attack lifecycle and demonstrate how each phase was identified using Elastic SIEM.

---

# 1️⃣ Brute Force

## Objective

Detect multiple failed authentication attempts.

### Query

```kql
event.code:4625
```

### Evidence

- Failed logon attempts
- Windows Security Event ID 4625

### MITRE ATT&CK

- T1110 – Brute Force

---

# 2️⃣ Initial Access

## Objective

Identify successful network authentication.

### Query

```kql
event.code:4624 AND winlog.event_data.LogonType:3
```

### Evidence

- Successful logon
- Network Logon (Type 3)

### MITRE

- T1078 – Valid Accounts

---

# 3️⃣ Privilege Escalation

## Objective

Detect privileged logons.

### Query

```kql
event.code:4672
```

### Evidence

- Administrative privileges assigned

### MITRE

- T1078

---

# 4️⃣ Persistence

## Objective

Detect local account creation.

### Query

```kql
event.code:(4720 OR 4732)
```

### Evidence

- User created
- User added to Administrators group

### MITRE

- T1136 – Create Account

---

# 5️⃣ Remote Execution

## Objective

Identify service creation and remote process execution.

### Query

```kql
event.code:(7045 OR 4688)
```

### Evidence

- Service installation
- Process creation

### MITRE

- T1059

---

# 6️⃣ Account Lockout

## Objective

Identify accounts locked due to repeated authentication failures.

### Query

```kql
event.code:4740
```

### Evidence

- User account locked

### Observation

This event demonstrates that the configured account lockout policy successfully mitigated the brute-force attack.

---

## 📊 Detection Coverage

| Attack Phase | Event IDs |
|--------------|-----------|
| Brute Force | 4625 |
| Account Lockout | 4740 |
| Initial Access | 4624 |
| Privilege Escalation | 4672 |
| Persistence | 4720 / 4732 |
| Remote Execution | 7045 / 4688 |
