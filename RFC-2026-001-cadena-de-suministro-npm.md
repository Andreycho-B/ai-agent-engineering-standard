# RFC-2026-001 — Cadena de suministro: scripts de instalación, lockfiles e integridad del historial Git

**Estado:** Provisional (periodo de observación, RFC-004)
**Fecha:** 2026-08-07
**Versión objetivo del estándar:** 1.1.0
**Documentos afectados:** 20. Seguridad (SEC-010), 30. Política de Control de Versiones (GIT-008), 31. Glosario (+4 términos), 25. Sistema de Auditoría (AUD-002)

---

## Problema

El ecosistema de instalación de dependencias es un vector de compromiso crítico que el estándar no aborda explícitamente:

1. **Scripts de instalación no auditados.** Los gestores de paquetes ejecutan scripts arbitrarios (`preinstall`, `install`, `postinstall`). Un paquete comprometido puede exfiltrar secretos, persistir malware o auto-replicarse sin dejar rastro en el código del proyecto.
2. **Lockfiles y transitividad opcionales.** Sin lockfile comprometido (con hashes) y sin pin exacto, las versiones flotantes permiten que una publicación futura maliciosa en el mismo rango envenene instalaciones existentes.
3. **Metadata de Git suplantable.** Autor, committer, fechas e identificadores pueden falsificarse; heredados como vector de ingeniería social para inyectar configuraciones de herramientas de IA (`.claude/`, `.vscode/tasks.json`, `settings.json`) que se ejecutan de forma automática.

## Evidencia

- **Cadena de suministro real (2025–2026).** Incidente de envenenamiento de la biblioteca `keyv` (proxy repo) y la variante **ChainDrop**: compromiso de un *maintainer*, payload difundido a 99M+ instalaciones semanales, con re-integración semiautónoma de comandos; tokens y secretos recolectados vía scripts `preinstall`. Documentado por Microsoft Threat Intelligence y firmas de seguridad (Snyk, Socket.dev, Elastic) en investigaciones públicas de 2025–2026. La respuesta recomendada fue restaurar y rotar todas las claves y re-verificar tokens en entornos expuestos.
- **Cadena de suministro agéntica.** El *Agentic AI Top 10* de OWASP (dic 2025) clasifica la **cadena de suministro agéntica** y la **ejecución de código inesperada** entre las categorías de riesgo principales de sistemas de agentes: un MCP, un *skill* (SKILL.md), un plugin o un script de instalación son componentes de suministro. El informe **"Engineering and Governing the Agent Harness"** (UNU-CPR, jul 2026) recomienda tratar *skills, MCP servers, plug-ins y tool wrappers como componentes de la cadena de suministro del software*.
- **Vector de herramientas de IA.** La familia de ataques del ecosistema (ChainDrop y variantes) inyecta configuraciones de herramientas (`.claude/settings.json` con `SessionStart`, `.vscode/tasks.json` con `folderOpen`) que ejecutan shell al abrir el proyecto. Vectores alineados con los programas de identidad y autorización de agentes iniciados por NIST (AI Agent Standards Initiative, feb 2026) y NCCoE.
- **Experiencia local.** El agente no dispone de reglas que le obliguen a auditar scripts de instalación, verificar un lockfile o tratar con confirmación explícita las configuraciones de herramientas de IA que se auto-ejecutan.

## Impacto

- Exfiltración de credenciales del entorno, de pipelines de CI, de registros de la máquina del desarrollador y de tokens de publicación de paquetes.
- Auto-replicación de malware en la cadena transitiva y entre proyectos (efecto combinatorio).
- Compromiso de la herramienta de desarrollo por ejecución automática de hooks, sin posibilidad de verificación con las directrices actuales: SEC-008 evalúa el riesgo al añadir una dependencia, pero no el proceso de instalación, ni la metadata histórica, ni los hooks de ejecución automática.
- Pérdida de confianza en la metadata de autoría como herramienta de revisión.

## Solución propuesta

Dos reglas nuevas de prioridad **CRÍTICA** y textos de soporte en glosario y auditoría:

1. **SEC-010 — Cadena de suministro de dependencias** (20. SEGURIDAD v2.0 → 2.1): auditoría previa de scripts de instalación (`preinstall`, `install`, `postinstall`), detención y reporte ante scripts anómalos, lockfile comprometido con hashes y versiones exactas, prohibición de rangos flotantes en producción, dependencias transitivas no correlacionadas tratadas como no confiables, instalación con scripts deshabilitados cuando la cadena no los exija, y protocolo de respuesta ante compromiso (pausa, aislamiento, rotación de secretos desde entorno limpio, auditoría de lockfile y logs del pipeline).

2. **GIT-008 — Verificación de autoría e integridad del historial** (30. POLÍTICA GIT v1.0 → v1.1): la metadata de autoría es suplantable y no constituye evidencia de confianza; commits triviales/automáticos fuera de tarea requieren verificación independiente; prohibición de ejecutar o persistir configuraciones de herramientas de IA auto-ejecutables (SessionStart, folderOpen, setup hooks) sin confirmación explícita; todo hallazgo de este tipo se reporta y nunca se sigue.

3. **31. GLOSARIO (v1.2 → v1.3):** términos *cadena de suministro de dependencias*, *hook de instalación*, *lockfile*, *compromiso de paquete* (definiciones descriptivas, GLO-004).

4. **25. SISTEMA DE AUDITORÍA (v1.2 → v1.3):** AUD-002 incorpora el quinto aspecto de verificación obligatoria: *superficie de ataque y cadena de suministro* (referencias SEC-010 y GIT-008).

Texto normativo completo de ambas reglas en los documentos afectados.

## Compatibilidad

- **Refuerza:** SEC-001 (verificación explícita), SEC-008 (auditoría previa de dependencias — ahora con nivel de detalle mecánico), SEC-009 (gates de CI: inspección de lockfile y logs en el mismo gate), GIT-002/GIT-007 (los hooks enumerados se auditan en la revisión pre-commit).
- **Sin duplicación verificada (RFC-003):** SEC-008 evalúa el riesgo al añadir la dependencia; SEC-010 regula el proceso de instalación (scripts, fijación, respuesta a incidentes). No se superponen ni se sustituyen.
- No modifica numeración de documentos ni añade capítulos.

## Riesgos

- **Falsos positivos:** paquetes legítimos con `postinstall` (binarios nativos) requerirán registro documentado; la regla exige auditoría, no prohibición.
- **Coste de disciplina en proyectos pequeños:** mitigable con la vía de instalación sin scripts cuando la cadena no lo exige.
- **Interpretación errónea de "no confiar en metadata":** la regla no elimina la firma ni la revisión; exige verificación de contenido cuando la metadata es la única fuente.
- **Cambio cultural** en el uso de skills/plugins de terceros: de confianza implícita a auditoría previa. Coste consciente del riesgo demostrado por los incidentes citados.

## Estado inicial

**Provisional** (RFC-004). Se mantiene en observación con las próximas versiones del estándar. Transición a **Estable** con evidencia acumulada de uso en entornos reales y sin desajustes con flujos de instalación legítimos. Transición a **Obsoleta** si el ecosistema incorpora garantías nativas de empaquetado y ejecución que lo sustituyan.

## Fuentes públicas

- OWASP. *Agentic AI Top 10* (diciembre 2025): ASI-04 *(Unexpected Code Execution)*, ASI-05 *(Agentic Supply Chain)*.
- UNU-CPR. *Engineering and Governing the Agent Harness* (julio 2026): skills, MCP servers, plug-ins y tool wrappers como componentes de cadena de suministro.
- Microsoft Threat Intelligence / firmas de seguridad (Snyk, Socket, Elastic). Análisis del incidente `keyv` / variante ChainDrop (2025–2026).
- NIST. *AI Agent Standards Initiative* (febrero 2026) y *NCCoE concept paper: identidad y autorización de agentes* (febrero 2026).
- IMDA (Singapur). *Model AI Governance Framework for Agentic AI* (enero 2026).
- Microsoft. *agent-governance-toolkit* (marzo 2026): MCP Security Gateway (tool poisoning, drift detection, hidden instructions).