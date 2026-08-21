# 🔍 Consultas de detección KQL

## 📌 Resumen general

Este documento contiene las consultas KQL (Kibana Query Language) usadas a lo largo de la investigación de la cadena de ataque completa simulada.

Las detecciones están organizadas según el ciclo de vida del ataque y demuestran cómo se identificó cada fase usando Elastic SIEM.

---

# 1️⃣ Fuerza bruta

## Objetivo

Detectar múltiples intentos de autenticación fallidos.

### Consulta

```kql
event.code:4625
```

### Evidencia

- Intentos de inicio de sesión fallidos
- Windows Security Event ID 4625

### MITRE ATT&CK

- T1110 – Brute Force

---

# 2️⃣ Acceso inicial

## Objetivo

Identificar autenticación exitosa vía red.

### Consulta

```kql
event.code:4624 AND winlog.event_data.LogonType:3
```

### Evidencia

- Inicio de sesión exitoso
- Logon de red (Type 3)

### MITRE

- T1078 – Valid Accounts

---

# 3️⃣ Escalada de privilegios

## Objetivo

Detectar inicios de sesión con privilegios.

### Consulta

```kql
event.code:4672
```

### Evidencia

- Privilegios administrativos asignados

### MITRE

- T1078

---

# 4️⃣ Persistencia

## Objetivo

Detectar creación de cuentas locales.

### Consulta

```kql
event.code:(4720 OR 4732)
```

### Evidencia

- Usuario creado
- Usuario agregado al grupo Administrators

### MITRE

- T1136 – Create Account

---

# 5️⃣ Ejecución remota

## Objetivo

Identificar creación de servicios y ejecución remota de procesos.

### Consulta

```kql
event.code:(7045 OR 4688)
```

### Evidencia

- Instalación de servicio
- Creación de proceso

### MITRE

- T1059

---

# 6️⃣ Bloqueo de cuenta

## Objetivo

Identificar cuentas bloqueadas por fallos de autenticación repetidos.

### Consulta

```kql
event.code:4740
```

### Evidencia

- Cuenta de usuario bloqueada

### Observación

Este evento demuestra que la política de bloqueo de cuentas configurada mitigó exitosamente el ataque de fuerza bruta.

---

## 📊 Cobertura de detección

| Fase del ataque         | Event IDs        |
|--------------------------|--------------------|
| Fuerza bruta              | 4625                |
| Bloqueo de cuenta         | 4740                |
| Acceso inicial            | 4624                |
| Escalada de privilegios   | 4672                |
| Persistencia              | 4720 / 4732         |
| Ejecución remota          | 7045 / 4688         |
