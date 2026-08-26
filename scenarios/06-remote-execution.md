# 🔵 Ejecución Remota
## 📌 Objetivo

Simular la ejecución remota de comandos a través de la creación de un servicio de Windows y validar la detección de instalación de servicios y ejecución de procesos utilizando Elastic SIEM.

---
## 🧠 Descripción del Ataque

Después de lograr acceso privilegiado y movimiento lateral, el atacante ejecutó comandos de forma remota en el endpoint objetivo mediante la creación de un servicio de Windows.
La ejecución generó eventos de Windows que indicaron tanto la instalación del servicio como la creación del proceso, confirmando que el código se ejecutó con privilegios elevados.
Esta etapa representa el control operativo total del endpoint comprometido.

---
## 🔍 Detección
### Query de Detección
```kql
event.code:(7045 OR 4688)
```
### Evidencia
- Creación de servicio de Windows (Event ID 7045)
- Ejecución de proceso (Event ID 4688)
- Ejecución bajo un contexto de seguridad privilegiado
---
## 📊 Indicadores de Compromiso (IOC)
- Nuevo servicio de Windows instalado
- Ejecución de proceso inesperada
- Ejecución bajo privilegios SYSTEM o administrativos
- Creación de servicio fuera de la actividad administrativa normal
---
## 🧩 Mapeo MITRE ATT&CK
| Táctica | Técnica | ID MITRE |
|--------|-----------|-----------|
| **Execution** | Service Execution | **T1569.002** |
> **Nota:** El Event ID 7045 confirma la creación de un servicio de Windows. El Event ID 4688 complementa la investigación aportando visibilidad sobre el proceso ejecutado.
---
## 📡 Fuentes de Evidencia
| Fuente | Evidencia |
|--------|----------|
| **Windows Security Logs** | Event ID 7045 (Creación de Servicio) |
| **Sysmon / Windows Logs** | Event ID 4688 (Creación de Proceso) |
| **Elastic SIEM** | Correlación de creación de servicio y ejecución de proceso |
| **Kibana** | Línea de tiempo de eventos de ejecución remota |
---
## 🚨 Evaluación del Analista

La creación de un nuevo servicio de Windows seguida de la ejecución de un proceso confirma que el atacante ejecutó código exitosamente en el endpoint comprometido.
Aunque la creación de servicios puede ocurrir durante la instalación legítima de software o la administración del sistema, la creación inesperada de un servicio después de la escalada de privilegios y el movimiento lateral debe considerarse altamente sospechosa.
Correlacionar estos eventos con las etapas previas del ataque brinda alta confianza en que el endpoint fue comprometido por completo.

---
## 💡 Lecciones Aprendidas
- La creación de servicios de Windows es un indicador de alto valor para detectar ejecución remota.
- Los eventos de creación de procesos proporcionan contexto adicional para comprender la actividad del atacante.
- Correlacionar la creación de servicios con eventos de autenticación y privilegios mejora significativamente la precisión de la investigación.
- La telemetría multi-fuente permite a los analistas reconstruir la ejecución remota con alta confianza.
