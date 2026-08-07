# RFC-2026-002 — Anexo de referencia: mapeo del capítulo 20 (Seguridad) contra el OWASP Top 10 for Agentic Applications

**Estado:** Provisional (periodo de observación, RFC-004)
**Fecha:** 2026-08-07
**Versión objetivo del estándar:** 1.1.1 (PARCHE, GV-006: contenido de referencia, sin cambio normativo)
**Documentos afectados:** 20. Seguridad (Anexo de mapeo), 32. Índice Maestro

---

## Problema

El estándar define reglas de seguridad propias (SEC-001..SEC-010) pero no publica su correspondencia con las taxonomías de amenazas reconocidas del ecosistema de agentes. Consecuencias:

1. **Auditoría sin referencia externa:** el Sistema de Auditoría (25) y la Política de Control de Versiones (30) verifican contra reglas internas, pero no pueden demostrar cobertura frente al estándar de referencia de la industria (OWASP Agentic Top 10), que es el lenguaje común con equipos de seguridad externos, CISOs y herramientas de evaluación (CSA AICM, MAESTRO, Microsoft AGT).
2. **Lagunas invisibles:** sin el mapeo no se distingue qué categorías de amenaza agéntica están cubiertas (cobertura directa), cuáles lo están parcialmente (por reglas de comportamiento de niveles 1–2) y cuáles quedan sin regla específica (candidatas a RFC futuras).
3. **Evaluadores y clientes no pueden verificar conformidad:** una tabla de mapeo permite a un tercero comprobar que el estándar aborda cada una de las diez categorías sin necesidad de leer los 32 documentos.

## Evidencia

- **OWASP GenAI Security Project.** *Top 10 for Agentic Applications (2026)*, publicado el 9 de diciembre de 2025, revisado por el *Agentic Security Initiative Expert Review Board* (con representantes de NIST, Comisión Europea y Alan Turing Institute). Diez categorías con designadores ASI01–ASI10: Agent Goal Hijack, Tool Misuse & Exploitation, Identity & Privilege Abuse, Agentic Supply Chain Vulnerabilities, Unexpected Code Execution, Memory & Context Poisoning, Insecure Inter-Agent Communication, Cascading Failures, Human-Agent Trust Exploitation, Rogue Agents.
- **Ecosistema de gobierno (2026):** el OWASP Agentic Top 10 es señalado por CSA (research note, abr 2026) como "el marco agéntico más accionable disponible" y base de *threat model* obligatoria para programas de gobierno de agentes; Microsoft *agent-governance-toolkit* (mar 2026) publica cobertura explícita de "10/10 ASI" como propiedad verificable de un sistema de gobierno.
- **Experiencia local:** RFC-2026-001 (v1.1.0) ya referenció ASI-04/ASI-05 como justificación de SEC-010/GIT-008; el mapeo general sistematiza esa relación para el resto de categorías.

## Impacto

- Imposibilidad de demostrar alineación con la taxonomía de amenazas más citada del sector; auditorías externas deben reinterpretar el estándar sin guía.
- Riesgo de solapamiento o laguna no detectada entre reglas (ej: ASI-07 *Insecure Inter-Agent Communication* no tiene regla de seguridad dedicada; hoy depende de 19. APIs y SEC-006/007).
- Sin tabla, cada futura RFC de seguridad debe rehacer el análisis de cobertura desde cero.

## Solución propuesta

Anexo **no normativo** (referencia) al final de **20. Seguridad**, titulado *Anexo A. Mapeo de referencia — SEC ⇄ OWASP Top 10 for Agentic Applications (2026)*, con una tabla que, para cada categoría ASI01–ASI10, indica: nombre oficial, descripción breve, reglas del estándar que la cubren (con ID), tipo de cobertura (Directa / Parcial — indirecta vía reglas de comportamiento — / No cubierta) y observaciones. La tabla distingue explícitamente cobertura de reglas SEC de niveles 3 y de reglas de comportamiento de niveles 1–2 (IRP, Epistémico, Contexto, Memoria, Auditoría), que es donde residen las mitigaciones de varias categorías agénticas.

El anexo declara su carácter informativo: no crea obligaciones nuevas (GV-005, no inflación normativa; GV-006, PARCHE) y no sustituye a los documentos normativos.

Cobertura esperada (a confirmar en el texto del anexo):

| Categoría OWASP | Tipo de cobertura | Reglas principales |
| :--- | :--- | :--- |
| ASI01 Agent Goal Hijack | Parcial (comportamiento) | 06 IRP, 12 Prompts, 13 Sesgos, 10 Matriz |
| ASI02 Tool Misuse & Exploitation | Parcial | SEC-003, GIT-006, 07 SSA |
| ASI03 Identity & Privilege Abuse | Directa | SEC-002, SEC-003, SEC-005, GIT-005 |
| ASI04 Agentic Supply Chain | Directa | SEC-008, SEC-010 |
| ASI05 Unexpected Code Execution | Directa | SEC-010, GIT-008, SEC-005 |
| ASI06 Memory & Context Poisoning | Parcial (comportamiento) | 08 Contexto, 24 Memoria, 09 PAP, GIT-008 |
| ASI07 Insecure Inter-Agent Communication | No cubierta (candidata RFC futura) | 19 APIs, SEC-006, SEC-007 |
| ASI08 Cascading Failures | Parcial | 21 Observabilidad/Resiliencia, 02 Convergencia |
| ASI09 Human-Agent Trust Exploitation | Parcial (comportamiento) | 12 Prompts, 05 Epistémico, AUD-001 |
| ASI10 Rogue Agents | Parcial (comportamiento) | 00 Constitución, 01 Protocolo, 02 Convergencia, AUD-003 |

## Compatibilidad

- No crea, modifica ni retira ninguna regla normativa (PARCHE, GV-006). Ningún identificador existente se altera (GV-003).
- No contradice GV-002 (no es una regla, es una tabla de referencia).
- Refuerza la trazabilidad exigida por 25. Sistema de Auditoría (AUD-002.5, cadena de suministro) y la Política de Control de Versiones (GIT-008).
- Identifica candidatos de cobertura para RFC futuras (ASI-07) sin incorporarlos ahora (RFC-002: no añadir sin evidencia de recurrencia).

## Riesgos

- **Percepción de cobertura falsa:** mitigado declarando el carácter de referencia del anexo y el tipo de cobertura por categoría (no se afirma que "el estándar cubre el Top 10").
- **Desactualización del anexo** si OWASP revisa la taxonomía (es un documento vivo): mitigado registrando el año/versión citada (2026) y colocándolo como anexo identificable.
- **Inflación documental:** minimizada al ser una única tabla dentro de un documento existente, sin documento nuevo.

## Estado inicial

**Provisional** (RFC-004). Pasará a **Estable** cuando exista evidencia de uso en auditorías y evaluaciones externas sin desajustes con la taxonomía OWASP vigente. **Obsoleta** si la taxonomía de referencia es sustituida por otra que lo requiera.

## Fuentes públicas

- OWASP GenAI Security Project. *Top 10 for Agentic Applications (2026)* (publicado 2025-12-09; revisado por el Expert Review Board con NIST, Comisión Europea, Alan Turing Institute).
- OWASP GenAI Security Project. *Agentic AI Threats and Mitigations* (taxonomía de amenazas y mitigaciones 1.1).
- CSA. *The AI Agent Governance Gap: What CISOs Need Now* (abril 2026): OWASP Agentic Top 10 como baseline de threat model.
- Microsoft. *agent-governance-toolkit* (marzo 2026): cobertura verificable "10/10 ASI" como propiedad de gobernanza.
- RFC-2026-001 (v1.1.0 del estándar): primer uso de ASI-04/ASI-05 como evidencia de reglas SEC-010/GIT-008.