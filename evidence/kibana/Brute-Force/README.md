# Evidencia de fuerza bruta

## Objetivo

Documentar los intentos de autenticación por fuerza bruta y el bloqueo de cuenta resultante.

## Evidencia

- Event ID 4625 — Múltiples intentos de autenticación fallidos.
- Event ID 4740 — Cuenta de usuario bloqueada tras superar el umbral configurado.

## Consultas de detección

```kql
event.code:4625
```

```kql
event.code:4740
```

## MITRE ATT&CK

- T1110 — Brute Force

## Observación

El evento de bloqueo de cuenta confirma que la política de seguridad configurada mitigó exitosamente el ataque de fuerza bruta, impidiendo temporalmente intentos de autenticación adicionales.
