# RFC-2026-003 — Catálogo de estéticas y firmas visuales reconocibles de IA (familia N del capítulo 14)

**Estado:** Provisional (periodo de observación, RFC-004)
**Fecha:** 2026-08-16
**Versión objetivo del estándar:** 1.2.0 (MENOR, GV-006: nuevas reglas compatibles que no rompen lo existente)
**Documentos afectados:** 14. Anti-patrones de Diseño Visual (nueva familia N), 32. Índice Maestro

---

## Problema

El capítulo 14 define principios contra interfaces genéricas, pero no cataloga las estéticas concretas que los modelos heredan del entrenamiento. Un agente puede detectar que un layout es "genérico", pero no dispone de un inventario de firmas para reconocerlas por nombre, distinguir sus señales observables y decidir entre justificarlas o eliminarlas. Las combinaciones más repetidas (Linear, DevTools/terminal, bento, v0/Shadcn, badge CI/CD, tipografía display) se replican sin que el agente tenga un criterio accionable.

## Evidencia

- **Recurrencia observada.** Las familias B, D y F documentan la repetición sistemática de recursos visuales como firma de IA. La producción de interfaces por agentes (2024–2026) confirma que las combinaciones se repiten con variación mínima entre proyectos y productos.
- **Origen identificable.** Cada firma procede de una fuente concreta y verificable: el aspecto de **Linear.app** (tarjeta oscura sobre lienzo claro); los indicadores de estado de **GitHub Actions** y **Vercel** (badge tipo CI/CD: punto/check, texto de estado, borde 1px, tinte alpha); el stack por defecto de **v0.dev**, **Lovable** y **Bolt.new** (Tailwind CSS + Shadcn UI, paleta Zinc/Slate, Inter/Geist); las fundiciones de fuentes display habituales en prototipos de IA (**Syne**, **Clash Display**, **Cabinet Grotesk**, **Monument Extended**).
- **Mecanismo.** Los generadores de UI y los LLM se entrenan con las mismas librerías y ejemplos (Shadcn, Tailwind, Radix, plantillas de landing) y convergen al mismo aspecto. Esa convergencia es observable y reproducible, no una impresión subjetiva.
- **Laguna del estándar.** El capítulo 14 carece de inventario de firmas; la aplicación de las familias B/D/F a estéticas concretas queda a interpretación del agente.

## Impacto

- Interfaces reconocibles como "generadas por IA" que erosionan la confianza del usuario y la identidad del producto.
- Sin inventario, cada agente aplica su propio umbral de detección; la verificación del capítulo 14 no es uniforme ni auditable.
- El Sistema de Auditoría (25) no puede verificar contra un catálogo objetivo si el documento no lo define.

## Solución propuesta

Nueva familia **N. Estéticas y firmas visuales reconocibles de IA** al final del capítulo 14 (v2.1 → v2.2), con 7 filas de firma (Patrón a evitar → Regla específica → Excepciones) que describen las señales observables de cada estética: Linear, DevTools/Developer-First, Bento Grid, v0/Shadcn, Status/Pill Badge tipo CI/CD, Brutalist Display y Editorial Bento/Neo-Brutalism. El texto normativo completo se incorpora al capítulo 14.

Las filas son **CRÍTICA** por defecto: su uso sin justificación explícita viola la regla. Heredan las Excepciones generales del capítulo (solicitud explícita del usuario, Design System del proyecto, justificación funcional/editorial/de marca, mejora objetiva de accesibilidad, o resultado objetivamente inferior).

Se añaden referencias cruzadas desde las familias B, D y F hacia la familia N (ARCH-004: referenciar, no duplicar). No se reescribe ningún principio existente.

## Compatibilidad

- No contradice reglas existentes (GV-001). Complementa las familias B (tendencias), D (tarjetas/repetición) y F (tipografía) por referencia.
- Sin duplicación (RFC-003): el principio general ya reside en B/D/F; la familia N aporta el inventario de señales, no un principio nuevo.
- No altera identificadores ni numeración (GV-003). Las notas de reestructuración del capítulo se actualizan.
- No añade documentos. Cambio MENOR (GV-006).

## Riesgos

- **Percepción de prohibir estéticas "modernas".** Mitigado: la regla prohíbe el uso por defecto no justificado, no las estéticas en sí; las excepciones generales y específicas por fila preservan el uso legítimo.
- **Inflación del capítulo.** Mitigado: una sola familia con tabla, sin una regla por cada señal anatómica.
- **Desactualización del catálogo.** Las firmas evolucionan; el catálogo es un inventario mínimo de las más recurrentes, revisable en futuras RFCs (RFC-004).

## Estado inicial

**Provisional** (RFC-004). Pasará a **Estable** cuando exista evidencia de uso en proyectos reales sin desajustes con Design Systems legítimos. **Obsoleta** si el ecosistema incorpora criterios nativos que lo sustituyan.

## Fuentes públicas

- **Linear.app.** Estética de origen de la firma "Linear" (tarjeta oscura sobre lienzo claro, bordes gris claro, acento de alto contraste).
- **v0.dev, Lovable, Bolt.new.** Generadores de UI por IA cuyo stack por defecto (Tailwind CSS + Shadcn UI) define la firma "v0/Shadcn".
- **Tailwind CSS, Shadcn UI, Radix.** Librerías de componentes que estandarizan el badge Soft/Subtle, la paleta Zinc/Slate y las tarjetas flotantes.
- **Vercel, GitHub Actions.** Indicadores de despliegue y placas de estado que originan el badge tipo CI/CD.
- **Fundiciones de fuentes display** (Syne, Clash Display, Cabinet Grotesk, Monument Extended): tipografías frecuentes en prototipos de IA.
