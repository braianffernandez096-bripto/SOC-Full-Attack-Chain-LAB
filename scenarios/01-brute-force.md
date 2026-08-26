# 🔴 Ataque de Fuerza Bruta
## 📌 Objetivo

Simular un ataque de fuerza bruta contra un endpoint Windows para generar múltiples intentos fallidos de autenticación y validar la capacidad del SIEM para detectar y correlacionar actividad de inicio de sesión sospechosa.

---
## 🧠 Descripción del Ataque

El atacante intentó repetidamente autenticarse en una cuenta de Windows utilizando credenciales inválidas en un corto período de tiempo.
Esta actividad generó múltiples eventos de inicio de sesión fallidos, proporcionando un indicador claro de comportamiento automatizado de adivinación de contraseñas.

---
## 🔍 Detección
### Query de Detección
```kql
event.code:4625
```
### Evidencia
- Múltiples intentos fallidos de autenticación
- Inicios de sesión repetidos dirigidos a la misma cuenta de usuario
- Alta frecuencia de autenticación en un intervalo corto de tiempo
---
## 📊 Indicadores de Compromiso (IOC)
- Alto volumen de intentos fallidos de inicio de sesión
- Fallos de autenticación repetidos contra la misma cuenta
- Eventos de autenticación ocurridos en un marco temporal corto
---
## 🧩 Mapeo MITRE ATT&CK
| Táctica | Técnica | ID MITRE |
|--------|-----------|-----------|
| **Credential Access** | Brute Force | **T1110** |
---
## 📡 Fuentes de Evidencia
| Fuente | Evidencia |
|--------|----------|
| **Windows Security Logs** | Event ID 4625 |
| **Elastic SIEM** | Correlación de eventos de autenticación |
| **Kibana** | Visualización en línea de tiempo de inicios de sesión fallidos |
---
## 🚨 Evaluación del Analista

Si bien los intentos fallidos de autenticación aislados son comunes en entornos empresariales, una secuencia sostenida de inicios de sesión fallidos dirigidos a la misma cuenta en un corto período de tiempo es un indicador fuerte de actividad de fuerza bruta.
En este laboratorio, los eventos generados fueron identificados y correlacionados exitosamente a través de Elastic SIEM, demostrando visibilidad sobre la etapa inicial del ataque.

---
## 💡 Lecciones Aprendidas
- Los eventos de autenticación fallida proporcionan indicadores valiosos para detectar ataques de contraseñas.
- Correlacionar intentos de autenticación a lo largo del tiempo mejora significativamente la precisión de la detección.
- Políticas adecuadas de bloqueo de cuenta ayudan a mitigar ataques de fuerza bruta antes de un compromiso exitoso.
