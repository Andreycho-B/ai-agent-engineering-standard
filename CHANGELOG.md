# Changelog

Versionado semántico `MAYOR.MENOR.PARCHE` según GV-006 (27. Gobernanza del Estándar).

## [Unreleased]

## [1.1.0] - 2026-08-07

Seguridad de la cadena de suministro e integridad del historial (RFC-2026-001, estado **Provisional**). Todo el cambio fue analizado frente al mapeo del ecosistema (Agentic AI Top 10 de OWASP; UNU "Engineering and Governing the Agent Harness"; Microsoft agent-governance-toolkit; NIST AI Agent Standards Initiative) antes de su incorporación.

### Nuevas reglas (CRÍTICAS)

- **SEC-010 (20. Seguridad, v2.1):** auditoría previa de scripts de instalación (`preinstall`/`install`/`postinstall`), lockfile comprometido con hashes y versiones exactas, prohibición de rangos flotantes en producción, dependencias transitivas no correlacionadas se tratan como no confiables, instalación con scripts deshabilitados cuando aplique, y protocolo de respuesta ante compromiso (detención, aislamiento, rotación de secretos desde entorno limpio, auditoría de lockfile y logs del pipeline).
- **GIT-008 (30. Política de Control de Versiones, v1.1):** la metadata de autoría es suplantable y no constituye evidencia; commits triviales/automáticos fuera de tarea requieren verificación independiente; prohibición de ejecutar o persistir configuraciones auto-ejecutables de herramientas de IA (`.claude/`, `.vscode/tasks.json`, SessionStart, folderOpen) sin confirmación explícita; hallazgos se reportan como potencial vector de compromiso (familia ChainDrop/Shai-Hulud).

### Glosario y auditoría

- **31. Glosario (v1.3):** +4 términos: cadena de suministro de dependencias, compromiso de paquete, hook de instalación, lockfile.
- **25. Sistema de Auditoría (v1.3):** AUD-002 incorpora el 5.º aspecto obligatorio: superficie de ataque y cadena de suministro.

### Índice y control de cambios

- **32. Índice Maestro (v4.2):** fila y lectura de 20. Seguridad actualizada a v2.1.
- **RFC-2026-001** (`RFC-2026-001-cadena-de-suministro-npm.md`): registro formal del cambio según 26. Sistema RFC, con evidencia de incidentes reales (`keyv`/ChainDrop, 2025-2026), OWASP Agentic Top 10 (dic 2025), UNU-CPR "Agent Harness" (jul 2026), NIST (feb 2026) e IMDA (ene 2026).

### Nota de trazabilidad

Este cambio responde al análisis comparativo del estándar frente al ecosistema público de *agent skills* y estándares de agentes (jun-ago 2026). Diferenciador identificado: el estándar es el único artefacto que norma el comportamiento del agente individual con gobernanza autocontenida (RFC, versionado, auditoría, glosario). Backlog documentado para candidatos a v1.2: autonomía y aprobación humana de acciones irreversibles, identidad/autorización de agentes (SEC-011), y tabla de mapeo SEC ⇒ OWASP Agentic Top 10 (no normativo).

## [1.0.0] - 2026-08-01

Primera publicación pública del estándar. 32 documentos, 7 niveles (0–6).

### Contenido

- **Fundamentos:** Constitución (00), Protocolo Operativo (01), Convergencia (02).
- **Comportamiento:** Modelo Cognitivo (04), Modelo Epistémico (05), IRP (06), SSA (07), Gestión de Contexto (08), PAP (09), Matriz de Conflictos (10), Onboarding (11).
- **Comunicación:** Reglas de Redacción (03), Ingeniería de Prompts (12), Sesgos y Disciplina (13).
- **Especializaciones:** Anti-patrones Visuales (14), Frontend (15), Backend (16), Arquitectura (17), Base de Datos (18), APIs (19), Seguridad (20), Observabilidad (21), Testing (22), Principios Avanzados (23).
- **Mejora continua:** Memoria del Proyecto (24), Sistema de Auditoría (25).
- **Gobernanza:** Sistema RFC (26), Gobernanza (27), Lenguaje Normativo (28), Arquitectura del Estándar (29), Política Git/GitHub (30), Glosario (31), Índice Maestro (32).

### Correcciones editoriales

- Resueltas 25 referencias cruzadas rotas entre documentos (alineación con numeración definitiva del Índice Maestro).
