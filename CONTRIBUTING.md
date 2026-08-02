# Contribuir

El estándar evoluciona únicamente mediante **RFC** (26. Sistema RFC). **Nunca se edita la especificación directamente** (RFC-001).

## Proceso

1. **Verifica** que el cambio no esté ya cubierto por una regla existente (RFC-003: fusionar antes de añadir).
2. **Abre una RFC** con los campos mínimos (RFC-001):
   - **Problema:** ¿qué problema existe?
   - **Evidencia:** ¿cómo se observó? ¿qué datos o experiencia lo respaldan?
   - **Impacto:** ¿qué consecuencias produce el problema actual?
   - **Solución propuesta:** ¿qué cambia exactamente? (texto de la nueva regla o modificación)
   - **Compatibilidad:** ¿qué reglas podrían verse afectadas, sustituidas u obsoletas?
   - **Riesgos:** ¿qué nuevos problemas podrían aparecer?
   - **Estado inicial:** Experimental → Provisional → Estable → Obsoleta
3. **Discute** la RFC en el issue hasta alcanzar consenso.
4. **No implementes** el cambio hasta que la RFC esté aprobada.

## Criterios de aceptación (RFC-002)

- La RFC cita **evidencia objetiva**, no preferencias personales.
- El beneficio supera claramente el coste introducido.
- Responde a un problema **recurrente**, no a un caso aislado.
- No contradice reglas existentes; si lo hace, marca la anterior como obsoleta y justifícalo (GV-001).

## Reglas de redacción

- Sigue **03. Reglas de Redacción**: densidad informativa, sin patrones LLM, sin relleno.
- Usa lenguaje normativo (28): `DEBERÁ`, `NO DEBERÁ`, `PODRÁ`, `DEBERÍA`.
- Mantén el formato de documento definido en **29. Arquitectura del Estándar**.
- Actualiza el **Índice Maestro (32)** con cualquier cambio estructural.

## Commits y pull requests

- Mensajes con formato `<tipo>(<alcance>): <descripción breve>` (GIT-003), ej: `fix(referencias): alinear numeración en 09`.
- Commits **atómicos** (un único cambio lógico por commit).
- Prohibido incluir secretos (GIT-002) o archivos excluidos (GIT-001).
- Antes del commit: verifica `git status` y `git diff --cached` (GIT-007).

## Reportes de seguridad

No reportes vulnerabilidades en issues públicos. Usa [SECURITY.md](SECURITY.md).
