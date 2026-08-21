# 🛡️ Informe del incidente — Análisis de cadena de ataque completa

## 📌 Resumen ejecutivo

Este informe documenta la investigación de un ciberataque simulado de múltiples etapas contra un endpoint Windows 10 dentro de un laboratorio SOC controlado.

El objetivo de la investigación fue reconstruir el ciclo de vida completo del ataque correlacionando telemetría de endpoint, Windows Security Events y evidencia de red recolectada a través de Elastic Stack, Sysmon, Winlogbeat y Wireshark.

El ataque consistió en intentos de autenticación por fuerza bruta, autenticación exitosa vía red, escalada de privilegios, persistencia, movimiento lateral a través de SMB, y ejecución remota de comandos.

---

## 🎯 Resumen general del incidente

| Categoría | Detalles |
|----------|---------|
| **Tipo de incidente** | Simulación de ataque multi-etapa |
| **Entorno** | Windows 10 • Kali Linux • Ubuntu (Elastic Stack) |
| **Plataforma de detección** | Elastic Stack (Elasticsearch y Kibana) |
| **Telemetría de endpoint** | Sysmon + Windows Security Logs |
| **Recolección de logs** | Winlogbeat |
| **Análisis de red** | Wireshark |
| **Framework** | MITRE ATT&CK |

---

## 🧠 Narrativa del ataque

El atacante inició un ataque de fuerza bruta contra una cuenta de usuario de Windows, generando múltiples intentos de autenticación fallidos.

Tras obtener credenciales válidas, se observó un inicio de sesión de red exitoso, permitiendo el acceso al endpoint objetivo.

Posteriormente se asignaron privilegios administrativos, habilitando acciones más allá de los permisos de un usuario estándar.

El atacante estableció persistencia creando una nueva cuenta local y agregándola al grupo local de Administrators.

Usando recursos administrativos compartidos SMB, se realizó ejecución remota mediante creación de servicios, resultando en ejecución de comandos en el endpoint comprometido.

La investigación reconstruyó cada etapa de la intrusión correlacionando logs de autenticación, telemetría de endpoint y tráfico de red.

---

## 🕒 Línea de tiempo del ataque

| Fase del ataque | Evidencia | Descripción |
|--------------|----------|-------------|
| **Fuerza bruta** | Event ID **4625** | Múltiples intentos de autenticación fallidos |
| **Acceso inicial** | Event ID **4624** | Inicio de sesión de red exitoso (Logon Type 3) |
| **Escalada de privilegios** | Event ID **4672** | Privilegios administrativos asignados |
| **Persistencia** | Event IDs **4720 / 4732** | Creación de usuario local y membresía en grupo de administradores |
| **Movimiento lateral** | SMB (TCP/445) | Comunicación a través de recursos administrativos compartidos |
| **Ejecución remota** | Event IDs **7045 / 4688** | Creación de servicio y ejecución de proceso |

---

## 📊 Resumen de la investigación

| Área de investigación | Resultado |
|--------------------|--------|
| Detección de fuerza bruta | ✅ Confirmado |
| Autenticación exitosa | ✅ Confirmado |
| Escalada de privilegios | ✅ Confirmado |
| Persistencia | ✅ Confirmado |
| Movimiento lateral | ✅ Confirmado |
| Ejecución remota | ✅ Confirmado |
| Correlación multi-fuente | ✅ Exitosa |

---

## 📡 Correlación de evidencia

La investigación combinó múltiples fuentes de telemetría para validar la actividad del atacante a lo largo del ciclo de vida del ataque.

| Fuente | Evidencia recolectada |
|--------|--------------------|
| **Elastic SIEM** | Eventos de autenticación, escalada de privilegios, ejecución de procesos y correlación de eventos |
| **Windows Security Logs** | Inicios de sesión fallidos, autenticación exitosa, inicios de sesión con privilegios, creación de cuentas |
| **Sysmon** | Creación de procesos y actividad del endpoint |
| **Wireshark** | Comunicaciones SMB y validación de red |

La combinación de telemetría de endpoint y evidencia de red permitió una reconstrucción completa del incidente.

---

## 🔍 Lógica de detección

Las siguientes consultas de detección fueron usadas durante la investigación.

| Consulta de detección | Propósito |
|-----------------|---------|
| `event.code:4625` | Detectar intentos de autenticación por fuerza bruta |
| `event.code:4624 AND winlog.event_data.LogonType:3` | Identificar inicios de sesión de red exitosos |
| `event.code:4672` | Detectar inicios de sesión con privilegios |
| `event.code:4720 OR event.code:4732` | Detectar persistencia mediante creación de cuentas |
| `event.code:7045 OR event.code:4688` | Identificar ejecución remota mediante creación de servicio y proceso |

---

## 🧩 Mapeo a MITRE ATT&CK

El comportamiento del atacante observado fue mapeado al framework MITRE ATT&CK.

| Táctica | Técnica | ID MITRE | Evidencia |
|--------|-----------|----------|----------|
| **Credential Access** | Fuerza bruta | **T1110** | Múltiples intentos de autenticación fallidos (Event ID 4625) |
| **Initial Access** | Cuentas válidas | **T1078** | Autenticación exitosa (Event ID 4624) |
| **Persistence** | Creación de cuenta | **T1136** | Creación de cuenta de administrador local (Event ID 4720) |
| **Lateral Movement** | SMB / Windows Admin Shares | **T1021.002** | Comunicación SMB (TCP/445) |
| **Execution** | Intérprete de comandos y scripts | **T1059** | Ejecución remota de comandos (Event ID 4688 / 7045) |

---

## 🚨 Evaluación de impacto

La investigación confirmó que el atacante simulado avanzó exitosamente a través de múltiples etapas del ciclo de vida del ataque, resultando en un compromiso completo del endpoint objetivo.

| Impacto | Evidencia |
|--------|----------|
| **Acceso no autorizado** | Autenticación exitosa tras múltiples inicios de sesión fallidos |
| **Escalada de privilegios** | Privilegios administrativos asignados (Event ID 4672) |
| **Persistencia** | Creación de cuenta de administrador local |
| **Movimiento lateral** | Actividad en recursos administrativos compartidos SMB |
| **Ejecución de comandos** | Creación de servicio y ejecución de proceso |

La correlación de eventos de autenticación, telemetría de endpoint y tráfico de red brindó un alto nivel de confianza en la reconstrucción del ataque.

---

## 🚨 Severidad del incidente

| Severidad | Evaluación |
|----------|------------|
| **Alta** | Acceso no autorizado confirmado, escalada de privilegios, persistencia, movimiento lateral y ejecución remota de comandos dentro del endpoint objetivo. |

---

## 💡 Lecciones aprendidas

Esta investigación reforzó la importancia de correlacionar múltiples fuentes de telemetría en lugar de depender de eventos aislados.

Observaciones clave incluyen:

- Los Windows Security Events brindan visibilidad sobre la actividad de autenticación y relacionada con privilegios.
- Sysmon mejora significativamente la visibilidad del endpoint al registrar la ejecución de procesos.
- El tráfico de red capturado con Wireshark complementa la telemetría del endpoint y valida el comportamiento del atacante.
- Mapear la actividad observada al framework MITRE ATT&CK mejora la documentación del incidente y la comunicación entre analistas.
- Construir una línea de tiempo de ataque estructurada simplifica la reconstrucción del incidente y respalda un análisis más rápido.

---

## 🔐 Recomendaciones

| Recomendación | Objetivo |
|---------------|-----------|
| Implementar políticas de bloqueo de cuentas | Reducir ataques de fuerza bruta |
| Monitorear inicios de sesión con privilegios (Event ID 4672) | Detectar escalada de privilegios |
| Restringir recursos administrativos compartidos SMB | Reducir oportunidades de movimiento lateral |
| Monitorear eventos de creación de servicios (Event ID 7045) | Detectar ejecución remota |
| Aplicar el Principio de Menor Privilegio | Limitar las capacidades del atacante |
| Mejorar las reglas de correlación del SIEM | Aumentar la cobertura de detección y reducir el tiempo de respuesta |

---

## 📌 Evaluación final

El incidente simulado demuestra cómo puede reconstruirse una cadena de ataque completa mediante la correlación de telemetría de endpoint, eventos de autenticación y evidencia de red.

En lugar de depender de alertas individuales, la investigación combinó múltiples fuentes de datos para lograr una comprensión integral del comportamiento del atacante.

Este proyecto refleja un flujo de trabajo práctico de investigación SOC y demuestra técnicas comúnmente utilizadas por analistas de Centros de Operaciones de Seguridad durante la respuesta a incidentes y la investigación de amenazas.
