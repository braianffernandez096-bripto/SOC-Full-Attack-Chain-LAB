# 📊 Resumen general de evidencia

Este directorio contiene la evidencia recolectada durante la investigación del ataque simulado.

Los artefactos incluidos en este repositorio respaldan los hallazgos documentados en el informe del incidente y demuestran cómo se correlacionaron múltiples fuentes de telemetría para reconstruir la cadena de ataque completa.

---

## 📁 Categorías de evidencia

### 🟣 Elastic SIEM (Kibana)

Evidencia recolectada desde Elastic Stack usada durante la investigación.

Ejemplos incluyen:
- Intentos de fuerza bruta (Event ID 4625)
- Autenticación exitosa (Event ID 4624)
- Inicios de sesión con privilegios (Event ID 4672)
- Creación de usuario (Event IDs 4720 / 4732)
- Creación de proceso (Event ID 4688)
- Creación de servicio (Event ID 7045)

Estas capturas ilustran cómo se identificaron la autenticación, escalada de privilegios, persistencia y ejecución de comandos a través de correlación en el SIEM.

---

### 🔵 Wireshark

Tráfico de red capturado durante la simulación del ataque.

La evidencia incluye:
- Comunicaciones SMB (TCP/445)
- Tráfico de autenticación
- Establecimiento de sesión
- Actividad de administración remota

El tráfico capturado complementa la telemetría del endpoint y valida el movimiento del atacante a través de la red.

---

### 🟡 Telemetría de endpoint

Evidencia a nivel de host recolectada a través de Sysmon y Windows Security Logs.

Ejemplos incluyen:
- Ejecución de procesos
- Instalación de servicios
- Creación de cuenta local
- Asignación de privilegios
- Eventos de autenticación

Esta telemetría brinda visibilidad sobre las acciones del atacante realizadas directamente en el endpoint comprometido.

---

## 🔍 Flujo de investigación

La investigación se realizó correlacionando múltiples fuentes de telemetría en lugar de depender de eventos individuales.

```text
Windows Security Logs
        │
        ▼
      Sysmon
        │
        ▼
 Elastic Stack (SIEM)
        │
        ▼
    Wireshark
        │
        ▼
Reconstrucción del ataque
```

---

## 🔒 Manejo de datos

Para proteger información sensible, se sanitizaron capturas seleccionadas.

La siguiente información puede estar parcialmente ofuscada:
- Direcciones IP internas
- Nombres de host
- Nombres de usuario
- Nombres de dominio (si aplica)

Esto no afecta la integridad de la investigación ni la lógica de detección presentada a lo largo del proyecto.
