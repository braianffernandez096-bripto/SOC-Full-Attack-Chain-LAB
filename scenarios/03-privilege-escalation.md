# 🟡 Escalada de Privilegios
## 📌 Objetivo

Simular el uso de privilegios elevados posterior a una autenticación exitosa y validar la detección de sesiones privilegiadas a través de Windows Security Events.

---
## 🧠 Descripción del Ataque

Después de autenticarse exitosamente en el sistema objetivo, el atacante obtuvo acceso a una cuenta privilegiada.
Windows generó un evento Special Logon (Event ID 4672), indicando que la sesión autenticada recibió privilegios administrativos.
Este evento representa un aumento significativo en las capacidades del atacante, habilitando acciones como persistencia, ejecución remota y movimiento lateral.

---
## 🔍 Detección
### Query de Detección
```kql
event.code:4672
```
### Evidencia
- Evento Special Logon (Event ID 4672)
- Privilegios administrativos asignados
- Sesión de usuario privilegiada establecida
---
## 📊 Indicadores de Compromiso (IOC)
- Sesión de inicio de sesión privilegiada
- Privilegios administrativos asignados
- Contexto de usuario elevado
- Secuencia de autenticación consistente con acceso privilegiado
---
## 🧩 Mapeo MITRE ATT&CK
| Táctica | Técnica | ID MITRE |
|--------|-----------|-----------|
| **Defense Evasion / Persistence / Privilege Context** | Valid Accounts | **T1078** |
> **Nota:** El Event ID 4672 indica que una sesión recibió privilegios especiales. En este laboratorio, se correlaciona con la autenticación exitosa previa (Event ID 4624) para demostrar la transición del atacante hacia un contexto privilegiado.
---
## 📡 Fuentes de Evidencia
| Fuente | Evidencia |
|--------|----------|
| **Windows Security Logs** | Event ID 4672 (Special Logon) |
| **Elastic SIEM** | Detección de eventos de inicio de sesión privilegiados |
| **Kibana** | Correlación de autenticación y asignación de privilegios |
---
## 🚨 Evaluación del Analista

El evento Special Logon confirma que la cuenta autenticada recibió privilegios elevados dentro del sistema operativo.
Aunque el Event ID 4672 por sí solo no indica actividad maliciosa, su correlación con el evento de autenticación exitosa y las etapas posteriores del ataque proporciona evidencia sólida de que el atacante operó con privilegios administrativos.

---
## 💡 Lecciones Aprendidas
- Los eventos de inicio de sesión privilegiados siempre deben investigarse dentro del contexto de la secuencia completa de autenticación.
- Correlacionar los Event ID 4624 y 4672 ayuda a identificar cuentas privilegiadas potencialmente comprometidas.
- Monitorear las sesiones administrativas proporciona visibilidad temprana sobre la actividad del atacante antes de que ocurra persistencia o movimiento lateral.
