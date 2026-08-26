# 🟣 Persistencia
## 📌 Objetivo

Simular persistencia mediante la creación de una nueva cuenta de usuario local y su incorporación al grupo local de Administradores, validando la detección de creación de cuentas no autorizadas y membresía en grupos privilegiados.

---
## 🧠 Descripción del Ataque

Después de obtener privilegios administrativos, el atacante estableció persistencia creando una nueva cuenta de usuario local y asignándole permisos administrativos.
Esta técnica permite el acceso continuo al sistema comprometido incluso si las credenciales originales son revocadas o el vector de ataque inicial es remediado.

---
## 🔍 Detección
### Query de Detección
```kql
event.code:(4720 OR 4732)
```
### Evidencia
- Nueva cuenta de usuario local creada (Event ID 4720)
- Usuario agregado al grupo local de Administradores (Event ID 4732)
---
## 📊 Indicadores de Compromiso (IOC)
- Creación de cuenta local no autorizada
- Usuario agregado al grupo de Administradores
- Cuenta privilegiada recién creada
- Cuenta administrativa que no sigue los procedimientos normales de aprovisionamiento
---
## 🧩 Mapeo MITRE ATT&CK
| Táctica | Técnica | ID MITRE |
|--------|-----------|-----------|
| **Persistence** | Create Account | **T1136** |
---
## 📡 Fuentes de Evidencia
| Fuente | Evidencia |
|--------|----------|
| **Windows Security Logs** | Event ID 4720 y 4732 |
| **Elastic SIEM** | Detección de eventos de creación de cuenta y membresía de grupo |
| **Kibana** | Correlación de actividad relacionada con persistencia |
---
## 🚨 Evaluación del Analista

La creación de una nueva cuenta local privilegiada indica un intento de establecer acceso a largo plazo al endpoint comprometido.
Aunque la creación de cuentas administrativas puede ser legítima en entornos empresariales, la creación inesperada de una cuenta seguida de su asignación inmediata al grupo de Administradores debe considerarse altamente sospechosa, particularmente cuando se correlaciona con eventos previos de autenticación, escalada de privilegios y movimiento lateral.

---
## 💡 Lecciones Aprendidas
- Monitorear la creación de cuentas locales es esencial para detectar mecanismos de persistencia.
- Los cambios en la membresía de grupos administrativos deben monitorearse y validarse de cerca.
- Correlacionar la creación de cuentas con etapas previas del ataque mejora significativamente la precisión de la investigación.
- Las técnicas de persistencia suelen aparecer después de que los atacantes obtienen acceso privilegiado, lo que hace que la correlación de eventos sea crítica durante la respuesta a incidentes.
