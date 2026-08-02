# AI Agent Engineering Standard

Especificación normativa de **32 documentos** que define el comportamiento de agentes de IA en tareas de ingeniería de software: cómo razonar, qué evidencia exigir, cuándo detener la iteración y qué reglas técnicas aplicar.

## ¿Qué problema resuelve?

Los agentes de IA producen resultados inconsistentes: responden con confianza sin evidencia, iteran sin criterio de parada, generan interfaces con "firma de IA" y violan principios de arquitectura, seguridad y testing. Este estándar convierte el comportamiento del agente en una especificación **auditable y verificable**, no en una lista de buenas intenciones.

## Estructura

7 niveles (0–6) y 32 documentos. El punto de navegación es el **Índice Maestro (32)**.

| Nivel | Contenido | Documentos |
| :--- | :--- | :--- |
| 0 | Constitución y principios superiores | 00 |
| 1 | Protocolo operativo, modelo cognitivo, contexto | 01, 02, 04–11, 24 |
| 2 | Reglas de redacción y comunicación | 03, 12, 13 |
| 3 | Especializaciones técnicas | 14–23 |
| 4 | Auditoría | 25 |
| 5 | Gobernanza y evolución | 26–30 |
| 6 | Glosario e índice | 31, 32 |

### Documentos

| ID | Nombre | Propósito |
| :--- | :--- | :--- |
| **00** | Constitución del Agente | Principios superiores e inquebrantables (evidencia sobre probabilidad). |
| **01** | Protocolo Operativo del Agente | Flujo obligatorio de ejecución (Recepción → Entrega). |
| **02** | Política de Convergencia | Cuándo detener iteraciones y dar por buena una solución. |
| **03** | Reglas de Redacción | Eliminar patrones LLM y maximizar densidad informativa. |
| **04** | Modelo Cognitivo | Cómo razonar (deliberativo, jerárquico, sistémico). |
| **05** | Modelo Epistémico | Cómo evaluar evidencia, conocimiento e incertidumbre. |
| **06** | Protocolo de Razonamiento Iterativo (IRP) | Loops de revisión interna (Comprensión → Autocrítica). |
| **07** | Sistema de Subagentes (SSA) | Roles especializados (Arquitecto, Backend, UX…). |
| **08** | Protocolo de Gestión del Contexto | Administrar memoria operativa y foco de la tarea. |
| **09** | Conciencia del Proyecto (PAP) | Comprender el sistema antes de intervenir. |
| **10** | Matriz de Resolución de Conflictos | Jerarquía de precedencia entre reglas. |
| **11** | Proyectos Nuevos y Contexto Inicial (Onboarding) | Procesar PRD, TRD y documentos de contexto. |
| **12** | Ingeniería de Prompts y Comunicación | Cómo preguntar, confirmar y manejar ambigüedad. |
| **13** | IA Generativa: Sesgos y Disciplina | Reconocer y corregir sesgos del modelo. |
| **14** | Anti-patrones de Diseño Visual | Evitar interfaces genéricas y "firma de IA". |
| **15** | Frontend Engineering | Reglas de componentes, estado y renderizado. |
| **16** | Backend Engineering | Reglas de dominio, servicios y lógica de negocio. |
| **17** | Arquitectura de Software | Estructura, capas, patrones y cohesión. |
| **18** | Base de Datos | Modelado, consultas, migraciones e integridad. |
| **19** | APIs y Contratos | Diseño de endpoints, versionado y compatibilidad. |
| **20** | Seguridad | Autenticación, autorización, cifrado y OWASP. |
| **21** | Observabilidad y Resiliencia | Logs, métricas, traces, timeouts, circuit breakers. |
| **22** | Testing Estratégico | Pirámide de pruebas, mocks, TDD, cobertura, mutación, UAT, gates de CI. |
| **23** | Principios de Ingeniería Avanzada | DDD, Hexagonal, SOLID, DRY/KISS/YAGNI, complejidad ciclomática. |
| **24** | Memoria y Mejora Continua | Decision Log, Known Problems, retrospectivas. |
| **25** | Sistema de Auditoría | Verificación final del cumplimiento del estándar. |
| **26** | Sistema RFC | Proceso formal para modificar el estándar. |
| **27** | Gobernanza del Estándar | Principios de evolución y estabilidad. |
| **28** | Lenguaje Normativo | Definición de DEBERÁ, NO DEBERÁ, PODRÁ… |
| **29** | Arquitectura del Estándar | Plantillas, identificadores y estructura documental. |
| **30** | Política de Git/GitHub | Secretos, commits, archivos de exclusión. |
| **31** | Glosario | Definiciones oficiales de términos técnicos. |
| **32** | Índice Maestro | Navegación y mapa global del estándar. |

## Cómo usar

**Con un agente de IA (recomendado):** apunta al agente a este repositorio e indica que adopte el estándar. El agente debe leer los documentos en el orden definido por el **flujo de lectura del Índice Maestro (32)** y cumplir la **Constitución (00)** y el **Protocolo Operativo (01)** en toda tarea.

**Como auditor humano:** usa el **Sistema de Auditoría (25)** para verificar que el trabajo del agente cumple el estándar antes de aceptarlo.

**Para aplicar reglas técnicas:** consulta las especializaciones (14–23). Cada regla incluye prioridad, regla normativa y método de verificación.

## Gobernanza

- El estándar evoluciona solo mediante **RFC** (26). No se edita directamente.
- Versionado semántico **MAYOR.MENOR.PARCHE** (27, GV-006).
- Lenguaje normativo obligatorio (28): `DEBERÁ`, `NO DEBERÁ`, `PODRÁ`.
- Términos definidos en el **Glosario (31)**.

## Contribuir

Consulta [CONTRIBUTING.md](CONTRIBUTING.md). Toda propuesta requiere RFC con: Problema, Evidencia, Impacto, Solución propuesta, Compatibilidad, Riesgos y Estado inicial.

## Seguridad

Reporta vulnerabilidades siguiendo [SECURITY.md](SECURITY.md). Prohibido publicar secretos o datos sensibles en issues públicos.

## Licencia

**Creative Commons Attribution 4.0 International (CC BY 4.0)** — ver [LICENSE](LICENSE).
