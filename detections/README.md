# Reglas de detección

Este directorio contiene las consultas de detección usadas a lo largo de la investigación.

Las reglas fueron creadas para identificar cada etapa del ataque simulado y están basadas en Windows Security Events y telemetría de Sysmon.

## Cobertura de detección

| Fase del ataque         | Detección               |
|--------------------------|--------------------------|
| Fuerza bruta              | Event ID 4625            |
| Acceso inicial            | Event ID 4624            |
| Escalada de privilegios   | Event ID 4672            |
| Persistencia              | Event IDs 4720 / 4732    |
| Ejecución remota          | Event IDs 7045 / 4688    |

Estas consultas están destinadas a fines educativos dentro de este laboratorio SOC.
