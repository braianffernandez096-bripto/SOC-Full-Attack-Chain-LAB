# 🟠 Acceso Inicial
## 📌 Objetivo

Simular una autenticación exitosa posterior a un ataque de fuerza bruta para validar la detección de credenciales comprometidas e identificar la transición entre intentos de inicio de sesión fallidos y acceso confirmado.
---
## 🧠 Descripción del Ataque
Después de múltiples intentos fallidos de autenticación, el atacante logró autenticarse exitosamente en el endpoint Windows objetivo utilizando credenciales válidas.
El inicio de sesión de red exitoso confirmó que el ataque de fuerza bruta resultó en un acceso no autorizado al sistema.
---
## 🔍 Detección
### Query de Detección
```kql
event.code:4624 AND winlog.event_data.LogonType:3
```
### Evidencia
- Autenticación de red exitosa
- Logon Type 3 (Inicio de Sesión de Red)
- Autenticación posterior a intentos repetidos de inicio de sesión fallidos
---
## 📊 Indicadores de Compromiso (IOC)
- Autenticación exitosa después de múltiples intentos fallidos
- Inicio de sesión de red (Type 3)
- Acceso obtenido utilizando credenciales válidas
- Secuencia de autenticación consistente con un compromiso por fuerza bruta
---
## 🧩 Mapeo MITRE ATT&CK
| Táctica | Técnica | ID MITRE |
|--------|-----------|-----------|
| **Initial Access** | Valid Accounts | **T1078** |
---
## 📡 Fuentes de Evidencia
| Fuente | Evidencia |
|--------|----------|
| **Windows Security Logs** | Event ID 4624 (Inicio de Sesión Exitoso) |
| **Elastic SIEM** | Correlación de eventos de autenticación |
| **Kibana** | Línea de tiempo mostrando autenticación exitosa posterior a inicios de sesión fallidos |
---
## 🚨 Evaluación del Analista
El inicio de sesión de red exitoso confirma que el atacante obtuvo credenciales válidas y logró un acceso no autorizado al sistema objetivo.
Al correlacionarse con los intentos fallidos de autenticación previos (Event ID 4625), este evento representa la transición de un ataque de credenciales a un compromiso confirmado.
---
## 💡 Lecciones Aprendidas
- Los eventos de inicio de sesión exitosos siempre deben analizarse en el contexto de la actividad de autenticación previa.
- Correlacionar los Event ID 4625 y 4624 mejora significativamente la detección de ataques de fuerza bruta exitosos.
- Monitorear los inicios de sesión de red ayuda a identificar accesos remotos no autorizados a sistemas Windows.
