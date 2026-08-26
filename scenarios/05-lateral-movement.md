# 🔵 Movimiento Lateral
## 📌 Objetivo

Simular movimiento lateral a través de recursos compartidos administrativos SMB y validar la detección de intentos de acceso remoto utilizando telemetría de endpoint y evidencia de red.

---
## 🧠 Descripción del Ataque

Tras la autenticación exitosa y el acceso privilegiado, el atacante intentó moverse lateralmente dentro del entorno interactuando con recursos compartidos administrativos SMB.
Se observó actividad de red sobre el puerto TCP 445 e intentos de acceso a recursos compartidos administrativos como **IPC$** y **C$** durante la investigación.

---
## 🔍 Detección
### Query de Detección
```kql
destination.port:445
```
> *Si tus logs de Sysmon lo soportan, podés reemplazarlo con:*
```kql
event.code:3 AND destination.port:445
```
### Evidencia
- Comunicaciones SMB sobre TCP/445
- Intentos de acceso a recursos compartidos administrativos
- Conexiones de red asociadas con administración remota
---
## 📊 Indicadores de Compromiso (IOC)
- Tráfico SMB sobre TCP/445
- Acceso a recursos compartidos administrativos (IPC$, C$)
- Conexiones SMB repetidas
- Actividad administrativa remota
---
## 🧩 Mapeo MITRE ATT&CK
| Táctica | Técnica | ID MITRE |
|--------|-----------|-----------|
| **Lateral Movement** | SMB/Windows Admin Shares | **T1021.002** |
---
## 📡 Fuentes de Evidencia
| Fuente | Evidencia |
|--------|----------|
| **Sysmon** | Eventos de conexión de red (Event ID 3) |
| **Elastic SIEM** | Correlación de actividad relacionada con SMB |
| **Wireshark** | Tráfico SMB sobre TCP/445 |
| **Kibana** | Línea de tiempo de actividad de red |
---
## 🚨 Evaluación del Analista

Las comunicaciones SMB observadas indican un intento de interactuar con recursos compartidos administrativos remotos después de haber obtenido acceso privilegiado.
Aunque los intentos de acceso no siempre resultan exitosos, este tipo de actividad es un indicador valioso de un posible movimiento lateral y debe investigarse en el contexto de los eventos previos de autenticación y privilegios.
La correlación entre eventos de autenticación, sesiones privilegiadas, telemetría de endpoint y tráfico de red refuerza la confianza en la reconstrucción de esta etapa del ataque.

---
## 💡 Lecciones Aprendidas
- El tráfico SMB debe monitorearse en busca de señales de administración remota no autorizada.
- La evidencia de red complementa la telemetría de endpoint al investigar movimiento lateral.
- El acceso a recursos compartidos administrativos es común en entornos empresariales, pero debe validarse contra el comportamiento del usuario y el historial de autenticación.
- Correlacionar la actividad SMB con etapas previas del ataque mejora la precisión de las investigaciones de incidentes.
