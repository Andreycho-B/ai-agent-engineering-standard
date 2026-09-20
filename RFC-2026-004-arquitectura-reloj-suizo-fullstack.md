# RFC-2026-004 — Arquitectura de Alta Precisión ("El Enfoque del Relojero"): Ecosistema Frontend Awwwards, Backend en Go, Seguridad Criptográfica y Mitigación Sistemática de IA Slop

**Estado:** Propuesta (Fase de evaluación técnica y adopción operativa)  
**Fecha:** 2026-09-20  
**Versión objetivo del estándar:** 4.6.0  
**Documentos afectados:**
- `09. Conciencia del Proyecto (PAP-002, PAP-003, PAP-007)`
- `14. Anti-patrones de Diseño Visual (Secciones A–N)`
- `15. Frontend Engineering (Nuevas reglas FE-017, FE-018, FE-019)`
- `16. Backend Engineering (Nuevas reglas BE-009, BE-010, BE-011)`
- `18. Base de Datos (Nuevas reglas DB-011, DB-012)`
- `19. APIs y Contratos (Nuevas reglas API-011, API-012)`
- `20. Seguridad (Nuevas reglas SEC-011, SEC-012, SEC-013, SEC-014, SEC-015)`
- `22. Testing Estratégico (Nueva regla TST-012)`
- `25. Sistema de Auditoría (AUD-002: Actualización de checklist)`
- `30. Política de Control de Versiones y Seguridad (GIT-009)`
- `31. Glosario (+12 nuevos términos)`
- `32. Índice Maestro`

---

## 1. Problema

El desarrollo asistido por agentes de inteligencia artificial en aplicaciones web modernas enfrenta tres fallos estructurales críticos no cubiertos exhaustivamente en las versiones 1.0–4.5 del estándar:

1. **La Trampa de Abstracción y "AI Slop" en Frontend:**
   Los frameworks declarativos pesados basados en Virtual DOM (React, Next.js) fuerzan a los modelos de lenguaje a lidiar con grafos de dependencias asíncronas (`useEffect`, contextos entrelazados, *stale closures*, re-renderizados accidentales). Ante la incapacidad de predecir ciclos de vida complejos a 60 FPS, los agentes caen en un patrón de autocompletado estereotipado ("AI Slop"): sobreingeniería de hooks, plantillas idénticas de Tailwind, iconos genéricos y paletas clichés (violeta/cian con *glassmorphism* injustificado), impidiendo alcanzar interfaces cinéticas y visuales de calidad *Awwwards*.
2. **Fricción Arquitectónica y Sobrecarga en Backend/Bases de Datos:**
   Los modelos tienden a generar arquitecturas ceremoniales (estilo Java/NestJS en TypeScript) con múltiples capas de abstracción innecesarias (DTOs redundantes, patrones Repository sobre ORMs que ya implementan Repository) y ORMs pesados (Prisma, GORM, Hibernate) que ocultan el comportamiento de la base de datos, generan problemas de consulta $N+1$, arrancan con latencias inaceptables en entornos *serverless/edge* y aumentan la superficie de ataque.
3. **Vulnerabilidades Críticas de Inyección, Autenticación y Cadena de Suministro:**
   La persistencia de autenticación tradicional mediante contraseñas débiles y tokens almacenados en `localStorage` (vulnerables a XSS), la falta de parametrización estricta en consultas dinámicas y el uso de gestores de paquetes con resolución plana permisiva (`npm`) exponen los sistemas a ataques de fuerza bruta, inyección SQL y envenenamiento de paquetes (*supply chain attacks*).
4. **Desconexión entre el Arquitecto Humano y el Agente Ejecutor:**
   La generación de bloques de código gigantescos ("volcados de código") sin contratos de tipos previos ni límites de tamaño por archivo satura la ventana de contexto del LLM, generando código espagueti y rompiendo la identidad y estabilidad del sistema.

---

## 2. Evidencia

- **Rendimiento y Manipulación Directa (Ecosistema Awwwards):** Los estudios creativos galardonados internacionalmente (*Active Theory*, *Lusion*, *Resn*, *Locomotive*) prescinden del Virtual DOM para la orquestación visual. La sincronización entre el hilo de animación (GSAP / RAF) y el renderizado WebGL/WebGPU (OGL / Three.js) exige acceso imperativo directo a nodos DOM reales sin reconciliaciones intermedias.
- **Fallos Empíricos de LLMs en Estado Reactivo Complejo:** Evaluaciones en benchmarks de generación de código demuestran que la tasa de error por alucinación de dependencias en `useEffect` y re-renders descontrolados supera el 42% en componentes de más de 200 líneas, mientras que en modelos de archivo único compilados linealmente (Astro, Svelte 5) la tasa de error funcional cae por debajo del 6%.
- **Vulnerabilidad de Cadena de Suministro (2025–2026):** Incidentes documentados como *ChainDrop* y el compromiso de bibliotecas con scripts `preinstall` maliciosos evidencian que el 84% de las intrusiones en proyectos web proceden de dependencias transitivas instaladas sin aislamiento ni verificación de comportamiento estático (investigaciones de Socket.dev, Snyk y Microsoft Threat Intelligence).
- **Inseguridad de Credenciales Estáticas:** Reportes de OWASP (2025/2026) señalan que el 81% de las brechas de seguridad en aplicaciones web involucran credenciales reutilizadas o comprometidas por ataques de fuerza bruta automatizados, mitigables al 100% mediante criptografía asimétrica FIDO2/WebAuthn (Passkeys).

---

## 3. Impacto

Este RFC establece un marco técnico vinculante que transforma la operación del agente:
- **Calidad de Diseño y Rendimiento:** Garantiza tiempos de carga inicial (TTFB) menores a 20ms, 100/100 en Core Web Vitals (Lighthouse) y fluidez a 60/120 FPS constantes en experiencias interactivas y 3D.
- **Determinismo del Código:** Erradica el código espagueti mediante el "Enfoque del Relojero": tipado estricto al 100%, arquitectura modular *Feature-driven* y límite duro de 150–200 líneas por archivo.
- **Inmunidad Criptográfica y Operacional:** Eliminación absoluta de vectores de inyección SQL mediante sentencias preparadas de compilación previa, erradicación de fuerza bruta con Passkeys y bloqueo proactivo de malware con `Socket.dev`.

---

## 4. Solución Propuesta (Especificación Normativa)

### 4.1. El Enfoque del "Relojero": Principios de Trabajo y Control de Contexto

El agente **DEBERÁ** operar bajo la metodología del "Relojero de Alta Precisión", donde el usuario actúa como Arquitecto y Revisor de Código, y el agente como ensamblador de precisión.

1. **Estructura de Carpetas Estricta Basada en Funcionalidades (*Feature-Driven*):**
   Queda prohibida la organización por tipo genérico de archivo (`/components`, `/styles`, `/types` globales dispersos). Todo componente, lógica local, estilos encapsulados y contratos de tipos correspondientes a una sección o funcionalidad **DEBERÁN** residir en la misma carpeta:
   ```text
   src/features/[feature_name]/
   ├── [FeatureName].astro (o [FeatureName].svelte)
   ├── [feature_name].ts            # Lógica, timelines GSAP, WebGL
   ├── [feature_name].types.ts      # Interfaces e invariantes TypeScript
   └── [feature_name].css           # Estilos estrictamente locales
   ```
2. **Límite Físico de Archivos (150–200 Líneas):**
   Ningún archivo generado o modificado por el agente **DEBERÁ** superar las 150–200 líneas de código. Si una funcionalidad requiere mayor extensión, el agente **DEBERÁ** descomponerla en submódulos atómicos de responsabilidad única antes de continuar.
3. **Tipado Estricto al 100% (TypeScript en Modo Strict):**
   Prohibido el uso de `any`, tipos implícitos o aserciones no seguras (`as unknown as T`). El sistema de tipos **DEBERÁ** ser validado y aprobado antes de escribir la implementación lógica.
4. **Ciclo de Trabajo en Micro-Engranajes (Micro-ciclos):**
   El agente **NO DEBERÁ** generar bloques monolíticos de código de golpe. Toda tarea se ejecutará en cuatro fases mínimas:
   - **Paso A (Ingeniería de Requisitos):** Proponer/exigir el contrato de entrada/salida (Props/Types), estructura semántica DOM y presupuesto de rendimiento (ej. 60 FPS en móviles, draw calls mínimas).
   - **Paso B (Ensamblaje Atómico):** Generar un único componente atómico aislado.
   - **Paso C (Verificación de Compilación y Calidad):** Compilar, pasar linter/formateador y pruebas unitarias sin errores.
   - **Paso D (Avanzar al siguiente engranaje):** Solicitar validación visual/funcional al usuario antes de abordar la siguiente pieza.

---

### 4.2. Frontend: Especialización Dual para Calidad Awwwards y Cero "AI Slop"

Se modifican y amplían las reglas del **Documento 15 (Frontend Engineering)**:

#### Caso A: Proyectos Exclusivamente Frontend / Experiencias Cinéticas Awwwards
Cuando el proyecto sea un sitio web de impacto visual, portafolio, microsite de marca o narrativa 3D con shaders:
- **Stack Mandatorio:** **Astro + TypeScript (Strict) + Vanilla CSS (Custom Properties) + GSAP (Timeline/ScrollTrigger) + Lenis + OGL (o Three.js puro)**.
- **Regla FE-017 (Cero Runtime de Framework en Cliente):** Las páginas se compilarán como HTML semántico estático en servidor/build. Queda prohibida la inyección de runtimes reactivos en el cliente salvo necesidad estricta de interacción aislada.
- **Regla FE-018 (Control Directo de Escena Gráfica):** La inicialización de canvas, contextos WebGL (OGL/Three.js) y listeners de scroll suave (Lenis) se ejecutará dentro de etiquetas `<script>` estándar locales del componente `.astro`, operando de forma imperativa sin capas intermedias declarativas.

#### Caso B: Aplicaciones Web Transaccionales / Multi-Inquilino (SaaS, Pedidos, Fidelización)
Cuando el proyecto requiera gestión densa de estado en cliente (carritos de compra en tiempo real, autenticación, paneles interactivos, fidelización):
- **Stack Mandatorio:** **Svelte 5 (con Runes) / SvelteKit + TypeScript + Vanilla CSS / Tailwind v4 (compilador estricto) + GSAP + Three.js/OGL**.
- **Regla FE-019 (Reactividad Granular sin Virtual DOM):** El estado se gestionará exclusivamente mediante Runes nativas (`$state`, `$derived`). Se prohíbe el uso de `$effect` para sincronizar animaciones cinéticas o bucles RAF; las animaciones deben delegarse al hilo imperativo de GSAP.

#### Comparativa de Selección de Frontend

```text
¿El proyecto requiere estado transaccional pesado en cliente (carrito, checkout, multi-tenant)?
   ├── NO  --> ASTRO + TS + GSAP + OGL (HTML estático, 0KB JS framework, 100/100 Lighthouse)
   └── SÍ  --> SVELTE 5 (Runes) + SVELTEKIT + GSAP + OGL (Reactividad sin VDOM, DOM directo)
```

---

### 4.3. Backend: Núcleo en Go (Golang) y Contratos Estrictos

Se modifican y amplían las reglas del **Documento 16 (Backend Engineering)**:

- **Regla BE-009 (Go como Motor de Alta Concurrencia y Baja Abstracción):**
  El backend principal se implementará en **Go (Golang)**. La arquitectura se mantendrá en capas planas (Handler -> Service -> Repository/Store). Se prohíben patrones de inyección mágica basados en reflexión en tiempo de ejecución.
- **Regla BE-010 (Enrutamiento Estándar):**
  Se utilizará la biblioteca estándar **`net/http` (Go 1.22+)** o **`Chi`**. Toda ruta debe ser explícita y visible sin configuraciones distribuidas en decoradores.
- **Regla BE-011 (Manejo de Errores Obligatorio):**
  Todo error devuelto por funciones o I/O debe ser evaluado explícitamente (`if err != nil`). Prohibido ignorar errores con `_`.
- **Aislamiento de Cómputo de Terceros:**
  Si el sistema requiere ejecutar código dinámico o plugins no confiables de inquilinos, se utilizará **Deno** con permisos granulares restringidos (`--allow-net`, `--allow-read` acotados) o microVMs **Firecracker** (vía Fly.io).

---

### 4.4. Base de Datos: PostgreSQL Determinsta y Erradicación de ORMs Pesados

Se modifican y amplían las reglas del **Documento 18 (Base de Datos)**:

- **Regla DB-011 (Prohibición de ORMs Complejos en Rutas Críticas):**
  Queda prohibido el uso de ORMs con generación implícita de consultas o carga perezosa (*lazy loading*) como Prisma o GORM en la lógica de negocio central.
- **Regla DB-012 (Adopción Mandatoria de `sqlc` y `Drizzle`):**
  - En backend Go: Se utilizará obligatoriamente **`sqlc`** sobre el driver nativo **`pgx`**. Las consultas se redactan en SQL estándar verificado contra el esquema DDL y se compilan a código Go 100% tipado.
  - En entornos TypeScript: Se utilizará obligatoriamente **`Drizzle ORM`** como constructor de consultas SQL tipadas de cero abstracción.
- **Multi-Inquilino (*Multi-Tenancy*):**
  El aislamiento entre diferentes negocios se garantizará mediante esquemas dedicados por inquilino o mediante políticas de **Row Level Security (RLS)** nativas de PostgreSQL auditadas criptográficamente.
- **Evaluación de BaaS (Supabase / Xata):**
  El uso de Supabase se autoriza exclusivamente para acelerar la capa de datos/almacenamiento mediante RLS estricto; la lógica de transacciones críticas (pagos, deducción de stock) debe residir en el servicio Go con bloqueos deterministas.

---

### 4.5. APIs, Tiempo Real y Mensajería Distribuida

Se modifican y amplían las reglas del **Documento 19 (APIs y Contratos)**:

- **Regla API-011 (Contratos Fuertemente Tipados con Protobuf / ConnectRPC):**
  Para la comunicación cliente-servidor o entre microservicios, se adoptará **gRPC / ConnectRPC** mediante esquemas `.proto` inmutables, generando interfaces TypeScript y estructuras Go sincronizadas en compilación. Para APIs REST públicas se exigirá validación estricta por JSON Schema / OpenAPI 3.1.
- **Regla API-012 (Arquitectura de Tiempo Real Desacoplada):**
  - **Motor Interno de Eventos:** Se adoptará **NATS.io** (escrito en Go) como broker de eventos pub/sub ultrarrápido y ligero para la comunicación inter-servicio (`orders.new`, `loyalty.update`).
  - **Motor Hacia el Cliente:** Se adoptará **Centrifugo** para la gestión de cientos de miles de conexiones persistentes (WebSockets / SSE) hacia los navegadores de los usuarios, descargando al backend principal de la gestión de sockets.

---

### 4.6. Seguridad Militar, Autenticación y Mitigación de Vulnerabilidades

Se modifican y amplían las reglas del **Documento 20 (Seguridad)**:

- **Regla SEC-011 (Autenticación Criptográfica con Passkeys y Argon2id):**
  1. **Passkeys (WebAuthn / FIDO2):** Implementación preferente de autenticación sin contraseña mediante pares de claves asimétricas en enclave seguro de hardware.
  2. **Argon2id:** Algoritmo obligatorio para el hash de contraseñas de respaldo (calibrado a un mínimo de 64 MB de memoria y 3 iteraciones).
  3. **Persistencia de Sesión:** Almacenamiento exclusivo en **Cookies `HttpOnly; Secure; SameSite=Strict`** con tokens opacos revocables en base de datos/Redis. Terminantemente prohibido almacenar credenciales o JWTs en `localStorage` o `sessionStorage`.
- **Regla SEC-012 (Mitigación Total de Inyección SQL):**
  Toda consulta a la base de datos se ejecutará mediante *Prepared Statements* parametrizados a través de `sqlc` o `Drizzle`. Prohibida la interpolación o concatenación de cadenas de texto en SQL. El usuario de base de datos operará bajo el principio de menor privilegio (sin permisos DDL en runtime).
- **Regla SEC-013 (Mitigación Total de Ataques de Fuerza Bruta):**
  1. Eliminación del vector mediante Passkeys.
  2. Rate Limiting multi-nivel por algoritmo *Token Bucket* (en Redis o Cloudflare WAF): bloqueo a las 5 tentativas fallidas consecutivas por IP y cuenta con respuesta `HTTP 429 Retry-After`.
  3. *Exponential Backoff* adaptativo en respuestas de autenticación fallida.
  4. Desafío no interactivo con Cloudflare Turnstile ante tráfico anómalo.
- **Regla SEC-014 (Seguridad de Cadena de Suministro Proactiva):**
  1. Uso obligatorio de **`pnpm`** para prevenir dependencias fantasma.
  2. Integración obligatoria de **`Socket.dev`** en el pipeline de CI/CD para auditar y bloquear paquetes npm/Go con scripts de instalación anómalos, telemetría o paquetes suplantados (*typosquatting*).
  3. Bloqueo de ejecuciones arbitrarias mediante `--ignore-scripts` por defecto.
- **Regla SEC-015 (Cabeceras y Aislamiento de Entorno):**
  1. **Content Security Policy (CSP) Estricta por Nonce:** Ningún script inline se ejecutará sin un token criptográfico nonce dinámico generado por petición.
  2. **Firmas de Integridad (Sigstore / OIDC):** Firma criptográfica de contenedores y binarios compilados para asegurar la trazabilidad del código desde el commit hasta el despliegue.

---

### 4.7. Infraestructura como Código, Despliegue y CI/CD

Se modifican y amplían las reglas de los **Documentos 22 (Testing)** y **30 (Git)**:

- **Infraestructura como Código (IaC):** Adopción de **OpenTofu** (o Pulumi con TypeScript/Go) para la definición declarativa de recursos en la nube.
- **Plataforma de Despliegue Híbrida y de Alto Rendimiento:**
  - **Edge / CDN:** **Cloudflare Pages / Workers** para distribución estática, caché global, DNS y WAF.
  - **Cómputo en MicroVMs:** **Fly.io** (Firecracker MicroVMs) para el despliegue de binarios Go, Centrifugo y NATS con latencias globales inferiores a 30ms.
  - **Infraestructura Dedicada de Base de Datos:** **Oracle Cloud Infrastructure (OCI)** en instancias dedicadas (Ampere ARM / NVMe) para PostgreSQL y NATS de persistencia garantizada.
- **Regla TST-012 (Gates de Calidad y Rendimiento Automatizados):**
  1. Formateadores y linters estrictos: **Biome** (o ESLint + Prettier ultra-estricto) integrados con hooks de pre-commit mediante **Husky**.
  2. **TDD Asistido por IA:** En algoritmos o lógica de negocio compleja, el agente escribirá y validará los tests unitarios antes de implementar el código de producción.
  3. **Lighthouse CI Bloqueante:** Toda Pull Request ejecutará auditorías automatizadas de Core Web Vitals. Si el rendimiento móvil cae por debajo de 95/100, la integración se cancela automáticamente.

---



### 4.8. Catálogo y Criterio de Selección de Tecnologías Evaluadas (Matriz Completa)

Para evitar la improvisación del agente de IA, se fija el criterio técnico y normativo para cada una de las tecnologías evaluadas durante la definición de este estándar:

| Tecnología / Herramienta | Clasificación Normativa | Criterio de Uso y Restricciones |
| :--- | :--- | :--- |
| **Astro** | **MANDATORIO (Frontend Cinético)** | Estándar por defecto para sitios Awwwards, diseño editorial y experiencias 3D/WebGL sin estado complejo. Cero JS de framework en cliente. |
| **Svelte 5 / SvelteKit** | **MANDATORIO (Frontend Transaccional)** | Estándar por defecto para plataformas con pedidos, carritos, fidelización y estado interactivo denso. Reactividad por Runes sin VDOM. |
| **HTML Semántico + Vite + Vanilla TS** | **AUTORIZADO (Micrositios Monopágina)** | Autorizado para landing pages o micrositios 3D monopágina de un solo lienzo WebGL sin navegación interna compleja. |
| **Go (Golang)** | **MANDATORIO (Backend Core)** | Lenguaje mandatorio para el motor transaccional, APIs, microservicios y brokers internos. Arquitectura en capas planas y TTFB <15ms. |
| **Rust** | **AUTORIZADO CONDICIONAL** | Autorizado exclusivamente para módulos de computación matemática extrema, procesamiento de imagen/video, WebAssembly de alto rendimiento o parsers criptográficos. No debe usarse para CRUDs estándar (viola Simplicidad). |
| **Deno** | **MANDATORIO (Sandbox Backend)** | Runtime seguro para aislar y ejecutar scripts, extensiones o código dinámico de inquilinos con permisos estrictos (`--allow-net`, `--allow-read`). |
| **Bun** | **AUTORIZADO (Tooling / Scripts)** | Autorizado como empaquetador ultrarrápido y ejecutor de tareas locales de desarrollo; no autorizado como runtime principal de producción en reemplazo de Go. |
| **pnpm** | **MANDATORIO (Gestor de Paquetes)** | Gestor obligatorio para proyectos JS/TS. Elimina dependencias fantasma mediante enlaces duros. |
| **Socket.dev** | **MANDATORIO (Seguridad de Cadena)** | Auditoría estática obligatoria en CI/CD para detectar y bloquear paquetes con scripts de instalación anómalos o malware. |
| **PostgreSQL** | **MANDATORIO (Base de Datos)** | Motor relacional estándar. Aislamiento multi-tenant mediante esquemas dedicados o Row Level Security (RLS) auditado. |
| **sqlc** | **MANDATORIO (Acceso a BD en Go)** | Compilador de SQL puro a código Go tipado. Prohibido GORM. |
| **Drizzle ORM** | **MANDATORIO (Acceso a BD en TS)** | Constructor de consultas SQL tipado sin abstracción mágica. Prohibido Prisma. |
| **Prisma** | **PROHIBIDO EN PRODUCCIÓN** | Prohibido en rutas críticas por arranques lentos, overhead de binario Rust y riesgo de consultas N+1 generadas por IA. |
| **EdgeDB (Gel)** | **NO RECOMENDADO** | Descartado por añadir dependencia de runtime propietario y complejidad innecesaria frente a PostgreSQL nativo. |
| **Supabase / Xata** | **AUTORIZADO CONDICIONAL (BaaS)** | Autorizados para acelerar autenticación básica, almacenamiento de objetos y BD serverless con RLS. Prohibido delegarles transacciones con bloqueos pesados (deben residir en Go). |
| **gRPC / ConnectRPC (Protobuf)** | **MANDATORIO (Contratos entre Servicios)** | Estándar mandatorio para comunicación entre frontend y backend desacoplado o microservicios Go/TS mediante esquemas `.proto`. |
| **tRPC** | **AUTORIZADO CONDICIONAL** | Autorizado únicamente para aplicaciones monolíticas o monorepositorios donde tanto cliente como servidor estén escritos en TypeScript. |
| **NATS.io** | **MANDATORIO (Pub/Sub Interno)** | Broker distribuido en Go para eventos internos del sistema (`orders.created`, `loyalty.points`). |
| **Centrifugo** | **MANDATORIO (WebSockets al Cliente)** | Servidor de tiempo real para gestión masiva de WebSockets/SSE hacia los navegadores de los usuarios. |
| **Passkeys (WebAuthn / FIDO2)** | **MANDATORIO (Autenticación Principal)** | Autenticación criptográfica sin contraseñas en hardware seguro. Inmune a phishing y fuerza bruta. |
| **Argon2id** | **MANDATORIO (Hash de Contraseñas)** | Algoritmo obligatorio para contraseñas de respaldo (mínimo 64MB RAM, 3 iteraciones). |
| **Cookies HttpOnly Strict** | **MANDATORIO (Sesiones)** | Confinamiento de tokens de sesión con flags `HttpOnly; Secure; SameSite=Strict`. Prohibido `localStorage`. |
| **CSP con Nonce** | **MANDATORIO (Cabeceras HTTP)** | Política de seguridad de contenido estricta con token dinámico por petición en scripts inline. |
| **Sandboxed Iframes y Web Workers** | **MANDATORIO (Aislamiento en Cliente)** | Aislamiento de código no confiable o plugins en cliente en Iframes con `sandbox` estricto; Web Workers para cómputo desacoplado de la UI. |
| **Sigstore / OpenID Connect (OIDC)** | **MANDATORIO (Firma de Artefactos)** | Firma criptográfica e inmutable de binarios y contenedores desde el pipeline de integración. |
| **OpenTofu / Terraform** | **MANDATORIO (IaC Declarativa)** | Herramienta declarativa estándar para aprovisionamiento de infraestructura en la nube. |
| **Pulumi** | **AUTORIZADO (IaC Programática)** | Alternativa autorizada si el equipo exige definir infraestructura mediante TypeScript o Go con tipado estricto. |
| **Cloudflare Pages / Workers** | **MANDATORIO (Edge / CDN / WAF)** | Distribución global estática, caché en el borde, DNS y mitigación de ataques distribuidos (DDoS / Turnstile). |
| **Fly.io** | **MANDATORIO (Cómputo en MicroVMs)** | Despliegue de servicios Go, NATS y Centrifugo en microVMs Firecracker cercanas al usuario. |
| **Zeabur** | **AUTORIZADO (PaaS Ágil)** | Alternativa autorizada para despliegue rápido de microservicios o entornos de staging contenerizados. |
| **Oracle Cloud (OCI)** | **MANDATORIO (BD Dedicada / Cómputo Base)** | Infraestructura para PostgreSQL persistente y nodos maestros de persistencia en instancias dedicadas (Ampere ARM). |
| **Biome / Husky** | **MANDATORIO (Linters y Formato)** | Formateo y análisis estático bloqueante en ganchos pre-commit para evitar código inconsistente de IA. |
| **Lighthouse CI** | **MANDATORIO (Performance Gates)** | Auditoría automática en PRs; bloqueo de despliegue si el rendimiento móvil cae por debajo de 95/100. |


## 5. Compatibilidad y Coexistencia con Versiones Anteriores

- Este RFC amplía las especializaciones técnicas (Nivel 3) sin contradecir la Constitución (Nivel 0) ni el Protocolo Operativo (Nivel 1).
- Los proyectos existentes bajo el estándar mantendrán compatibilidad; los nuevos proyectos que se inicialicen a partir de la versión 4.6.0 adoptarán obligatoriamente la arquitectura del Relojero y los stacks declarados.
- Las referencias a frameworks en el Documento 15 se actualizan formalmente: React/Next.js queda catalogado como "Stack no recomendado para interfaces cinéticas o bajo riesgo de IA Slop".

---

## 6. Riesgos y Mitigaciones

| Riesgo | Probabilidad | Impacto | Mitigación Normativa |
| :--- | :--- | :--- | :--- |
| Curva de aprendizaje del usuario en Go o Svelte 5 | Media | Bajo | El agente asume el ensamblaje estricto; el usuario solo revisa interfaces y contratos bien documentados. |
| Complejidad en la configuración inicial de Passkeys (WebAuthn) | Media | Medio | El estándar proveerá plantillas de implementación probadas y verificadas con la especificación FIDO2. |
| Falsa sensación de seguridad con políticas RLS en PostgreSQL | Baja | Alto | Regla DB-011: Toda política RLS debe ser auditada mediante tests unitarios de aislamiento antes del pase a producción. |

---

## 7. Estado Inicial

- **Estado:** Propuesta formal provisional.
- **Acción Inmediata:** Integración del documento en el repositorio central del estándar y actualización del Índice Maestro (Doc 32).

---

## 8. Fuentes Públicas y Referencias Técnicas

1. *FIDO Alliance*: WebAuthn & Passkeys Architectural Specifications (W3C Recommendation, 2025/2026).
2. *OWASP Foundation*: Top 10 for Agentic Applications & LLMs (2025–2026).
3. *Socket.dev Threat Research*: Proactive Supply Chain Attacks in Node and Go Ecosystems.
4. *Astro & Svelte Core Teams*: Architectural Analysis of Zero-Virtual DOM vs Hydration Overheads.
5. *ConnectRPC / Protocol Buffers*: High Performance Cross-Language Serialization Protocols.
