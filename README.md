# SOC-Full-Attack-Chain-LAB
Laboratorio de ataque en cadena completo para SOC

Laboratorio SOC que simula un ataque en cadena completo (detección mediante Elastic Stack: fuerza bruta, movimiento lateral, ejecución remota) que incluye:

🛡️ Laboratorio de ataque en cadena completo para SOC — Detección de extremo a extremo

📌 Descripción general

Este proyecto simula un ataque en cadena completo desde la perspectiva de un SOC (Centro de Operaciones de Seguridad), centrándose en la detección y el análisis del comportamiento del atacante.

El laboratorio se construyó utilizando Elastic Stack (SIEM), Sysmon y Winlogbeat, con un endpoint Windows 10 (máquina cliente) y Kali Linux como máquina atacante.

🧠 Escenario

El ataque comienza con un intento de fuerza bruta contra un sistema Windows, seguido de una autenticación exitosa, escalada de privilegios, movimiento lateral mediante SMB y ejecución remota.

El objetivo es detectar y correlacionar cada etapa utilizando el SIEM y el análisis de red.

🔴 Etapas del ataque

Fuerza bruta (ID de evento 4625)

Inicio de sesión exitoso (ID de evento 4624)

Escalada de privilegios (ID de evento 4672)

Creación de usuario y persistencia (ID de evento 4720 / 4732)

Movimiento lateral mediante SMB (Puerto 445)

Ejecución remota (ID de evento 7045 / 4688)

📡 Enfoque de detección

La detección se realizó utilizando:

Elastic SIEM (correlación de registros)

Sysmon (telemetría de endpoint)

Wireshark (análisis de red)

🧩 MITRE ATT&CK

T1110 — Fuerza bruta

T1078 — Cuentas válidas

T1021 — Servicios remotos

T1059 — Ejecución de comandos

T1136 — Creación de cuentas

🚨 Impacto

El atacante logró:

Acceso no autorizado

Escalada de privilegios

Movimiento lateral

Ejecución remota de código

👉 Compromiso total del endpoint. 💡 Conclusión

Este laboratorio demuestra cómo se puede reconstruir una cadena de ataque completa correlacionando eventos de múltiples fuentes de datos.
