# SOC-Full-Attack-Chain-LAB

Laboratorio de Cadena de Ataque Completa para SOC

[![Status](https://img.shields.io/badge/Status-Completed-brightgreen)](https://img.shields.io/badge/Status-Completed-brightgreen) [![Platform](https://img.shields.io/badge/Platform-Windows%2010-blue)](https://img.shields.io/badge/Platform-Windows%2010-blue) [![SIEM](https://img.shields.io/badge/SIEM-Elastic%20Stack-purple)](https://img.shields.io/badge/SIEM-Elastic%20Stack-purple) [![Sysmon](https://img.shields.io/badge/Telemetry-Sysmon-blue)](https://img.shields.io/badge/Telemetry-Sysmon-blue) [![Winlogbeat](https://img.shields.io/badge/Log%20Forwarder-Winlogbeat-orange)](https://img.shields.io/badge/Log%20Forwarder-Winlogbeat-orange) [![KQL](https://img.shields.io/badge/Detection-KQL-blue)](https://img.shields.io/badge/Detection-KQL-blue) [![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-Mapped-red)](https://img.shields.io/badge/MITRE%20ATT%26CK-Mapped-red) [![Wireshark](https://img.shields.io/badge/Network%20Analysis-Wireshark-blue)](https://img.shields.io/badge/Network%20Analysis-Wireshark-blue)

Un laboratorio SOC que simula una cadena de ataque completa (detección vía Elastic Stack: fuerza bruta, movimiento lateral, ejecución remota), que incluye:

🛡️ Laboratorio de Cadena de Ataque Completa para SOC — Detección de Punta a Punta

📌 Resumen general

Este proyecto simula una cadena de ciberataque completa desde la perspectiva de un Centro de Operaciones de Seguridad (SOC), enfocándose en la detección de amenazas, correlación de eventos e investigación de incidentes usando el Elastic Stack.

---

## 🏗️ Arquitectura del laboratorio

El laboratorio fue diseñado para simular un entorno empresarial realista donde la telemetría de endpoints y el tráfico de red pueden recolectarse, centralizarse y analizarse a través de un SIEM.

```
                 Kali Linux
                      │
      Simulaciones SMB / PowerShell / HTTP
                      │
                      ▼
+-----------------------------------------------+
| Windows 10 Víctima                             |
| • Sysmon                                       |
| • Winlogbeat                                   |
| • Windows Security Logs                        |
+-----------------------------------------------+
                      │
             Recolección de logs
                      │
                      ▼
+-----------------------------------------------+
| Servidor Ubuntu                                |
| • Elasticsearch                                |
| • Kibana                                       |
| • Elastic Stack                                |
+-----------------------------------------------+
```

### Entorno

| Máquina             | Rol                | Componentes principales                     |
| -------------------- | ------------------ | -------------------------------------------- |
| **Kali Linux**       | Atacante           | Simulaciones de ataque (SMB, PowerShell, HTTP) |
| **Windows 10**       | Endpoint víctima   | Sysmon, Winlogbeat, Windows Security Logs     |
| **Servidor Ubuntu**  | Plataforma SIEM    | Elasticsearch, Kibana                         |

### Flujo de datos

```
Simulación de ataque
        │
        ▼
Endpoint Windows
        │
Sysmon + Windows Security Logs
        │
Winlogbeat
        │
Elasticsearch
        │
Kibana
        │
Detección e investigación
```

## 🧠 Escenario

El objetivo de este laboratorio fue simular un ataque realista contra un endpoint Windows y reconstruir cada etapa de la intrusión usando telemetría del endpoint y evidencia de red.

La investigación se centró en correlacionar Windows Security Events, telemetría de Sysmon, detecciones del SIEM de Elastic y capturas de paquetes de Wireshark para identificar la actividad del atacante a lo largo de todo el ciclo de vida del ataque.

## 🕒 Línea de tiempo del ataque

La siguiente línea de tiempo resume la progresión del ataque observada durante la investigación.

```
Fuerza bruta
      │
      ▼
Autenticación exitosa
      │
      ▼
Escalada de privilegios
      │
      ▼
Persistencia
      │
      ▼
Movimiento lateral (SMB)
      │
      ▼
Ejecución remota
```

| Fase del ataque                | Evidencia                                |
| ------------------------------- | ----------------------------------------- |
| **Fuerza bruta**                | Windows Security Event ID 4625            |
| **Autenticación exitosa**       | Windows Security Event ID 4624            |
| **Escalada de privilegios**     | Windows Security Event ID 4672            |
| **Persistencia**                | Windows Security Event IDs 4720 / 4732    |
| **Movimiento lateral**          | Tráfico SMB (TCP/445)                     |
| **Ejecución remota**            | Event ID 4688 / 7045                      |
| **Comando y control**           | Sysmon Event ID 3 + Wireshark             |

---

## 🔍 Lógica de detección

En lugar de depender de una sola alerta, la investigación se centró en correlacionar múltiples fuentes de telemetría para reconstruir la cadena de ataque.

Las siguientes fuentes de datos fueron analizadas a lo largo de la investigación:

| Fuente de datos          | Propósito                                                          |
| -------------------------- | -------------------------------------------------------------------- |
| Windows Security Logs      | Eventos de autenticación, escalada de privilegios, creación de cuentas |
| Sysmon                     | Creación de procesos y conexiones de red                             |
| Elastic SIEM                | Correlación de eventos y reconstrucción de línea de tiempo          |
| Wireshark                  | Validación de tráfico de red y análisis de protocolos                |

### Flujo de detección

1. Se identificaron múltiples intentos de autenticación fallidos a través del Windows Security Event ID **4625**.

2. Un inicio de sesión exitoso (Event ID **4624**) del mismo usuario indicó que se habían obtenido credenciales válidas.

3. Se confirmaron privilegios administrativos usando el Event ID **4672**, lo que sugiere escalada de privilegios.

4. Los eventos de creación de cuenta (**4720**) y cambios de membresía de grupo (**4732**) revelaron mecanismos de persistencia.

5. La creación de procesos y actividad de red recolectada por Sysmon se correlacionó con el tráfico SMB capturado en Wireshark para validar la ejecución remota y el movimiento del atacante.

Esta correlación permitió reconstruir la cadena de ataque completa con un alto nivel de confianza.

### Flujo de investigación

```
Windows Security Logs
          │
          ▼
       Sysmon
          │
          ▼
     Elastic SIEM
          │
          ▼
     Wireshark
          │
          ▼
Reconstrucción del ataque
```

---

## 🧩 Mapeo a MITRE ATT&CK

El ataque simulado fue mapeado al framework MITRE ATT&CK para clasificar las tácticas y técnicas del adversario observadas durante la investigación.

| Táctica                  | Técnica                                | ID MITRE       | Evidencia                                                    |
| -------------------------- | ---------------------------------------- | --------------- | -------------------------------------------------------------- |
| **Credential Access**      | Fuerza bruta                             | **T1110**        | Múltiples intentos de autenticación fallidos (Event ID 4625)  |
| **Initial Access**         | Cuentas válidas                          | **T1078**        | Autenticación exitosa (Event ID 4624)                          |
| **Persistence**            | Creación de cuenta                       | **T1136**        | Cuenta de administrador local creada (Event ID 4720)           |
| **Lateral Movement**       | Servicios remotos (SMB)                  | **T1021.002**    | Tráfico SMB (TCP/445) y ejecución remota                       |
| **Execution**              | Intérprete de comandos y scripts         | **T1059**        | Ejecución remota de proceso (Event ID 4688 / 7045)             |

### Cobertura MITRE

Este laboratorio demuestra cómo pueden identificarse múltiples técnicas de ATT&CK correlacionando telemetría de endpoint, eventos de autenticación y tráfico de red, brindando mayor visibilidad sobre el ciclo de vida del ataque.

---

## 📊 Habilidades demostradas

Este proyecto demuestra experiencia práctica en múltiples áreas de Operaciones de Seguridad (SOC), incluyendo monitoreo de endpoints, correlación de eventos, detección de amenazas e investigación de incidentes.

| Categoría                      | Habilidades demostradas                       |
| --------------------------------- | ------------------------------------------------ |
| **SIEM**                          | Elastic Stack (Elasticsearch y Kibana)           |
| **Monitoreo de endpoints**        | Sysmon                                            |
| **Recolección de logs**           | Winlogbeat                                        |
| **Detección de amenazas**         | Análisis de comportamiento y correlación de eventos |
| **Investigación de incidentes**   | Reconstrucción de línea de tiempo del ataque      |
| **Análisis de red**               | Análisis de paquetes con Wireshark                |
| **Análisis de autenticación**     | Investigación de Windows Security Events          |
| **Frameworks**                    | Mapeo a MITRE ATT&CK                              |

### Competencias principales

- Monitoreo de seguridad
- Detección de amenazas
- Correlación de eventos
- Investigación de incidentes
- Análisis de telemetría de endpoints
- Análisis de tráfico de red
- Identificación de IOCs
- Mapeo a MITRE ATT&CK

---

## 🚨 Evaluación de impacto

La investigación confirmó que el atacante simulado avanzó exitosamente a través de múltiples etapas del ciclo de vida del ataque, resultando en un compromiso completo del endpoint objetivo.

Se observaron las siguientes actividades durante la investigación:

| Impacto                          | Evidencia                                                                                            |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Acceso no autorizado**            | Autenticación exitosa tras múltiples intentos de inicio de sesión fallidos (Event ID 4624)               |
| **Escalada de privilegios**         | Privilegios administrativos asignados (Event ID 4672)                                                     |
| **Persistencia**                    | Cuenta de administrador local creada y agregada al grupo Administrators (Event IDs 4720 / 4732)           |
| **Movimiento lateral**              | Comunicaciones SMB y actividad de ejecución remota                                                        |
| **Ejecución de comandos**           | Eventos de creación de procesos y ejecución de servicios (Event ID 4688 / 7045)                           |

### Evaluación de seguridad

El ataque demuestra cómo un adversario puede pasar de un acceso inicial a un compromiso completo del endpoint encadenando múltiples técnicas.

La investigación también resalta el valor de correlacionar telemetría de endpoint, eventos de autenticación y evidencia de red para reconstruir con precisión la actividad del atacante a lo largo del incidente.

---

## 💡 Lecciones aprendidas

Este proyecto reforzó la importancia de analizar incidentes de seguridad a través de la correlación de múltiples fuentes de telemetría, en lugar de depender de eventos aislados.

Algunos de los aprendizajes clave de este laboratorio incluyen:

- Correlacionar Windows Security Events con telemetría de Sysmon brinda mayor visibilidad sobre la actividad del atacante.
- La evidencia de red recolectada con Wireshark complementa la telemetría del endpoint y ayuda a validar el comportamiento del atacante.
- Mapear la actividad observada al framework MITRE ATT&CK mejora la documentación y comunicación del incidente.
- Construir una línea de tiempo de ataque estructurada simplifica la investigación del incidente y respalda una toma de decisiones más rápida durante el análisis.

En conjunto, este laboratorio fortaleció habilidades prácticas en detección de amenazas, correlación de eventos e investigación de incidentes dentro de un entorno SOC.

---

## 📄 Documentación

La documentación técnica adicional de este proyecto está disponible en el directorio `docs/`.

- **Informe completo del incidente** – Investigación completa, correlación de evidencia, evaluación de impacto y recomendaciones.
- **Consultas de detección** – Consultas KQL usadas durante la investigación.
- **Escenario de ataque** – Descripción detallada de la cadena de ataque simulada.
