# Política de Seguridad

## Reportar una vulnerabilidad

**NO abras un issue público para reportar vulnerabilidades.** La divulgación pública prematura expone a los usuarios y viola la política de seguridad del estándar (20. Seguridad, 30. Política Git/GitHub).

### Cómo reportar

1. Abre un reporte privado mediante **GitHub Security Advisories** (pestaña *Security* del repositorio) o escribe a los mantenedores por canal privado.
2. Incluye:
   - Documento afectado (ID y nombre) y versión.
   - Descripción del problema.
   - Impacto potencial.
   - Pasos de reproducción o evidencia.
3. No publiques el hallazgo públicamente hasta que se haya aplicado una corrección o hayan pasado 90 días sin respuesta.

### Qué se considera vulnerabilidad

- Contenido que pueda inducir a agentes a ejecutar acciones dañinas (prompt injection, exfiltración).
- Reglas o plantillas que comprometan secretos, credenciales o datos sensibles.
- Errores normativos que contradigan la Constitución (00) o la Política de Seguridad (20).

### Qué NO es una vulnerabilidad

- Errores tipográficos o referencias rotas (reportar como RFC editorial o issue normal).
- Preferencias estilísticas.

## Compromiso de respuesta

| Plazo | Acción |
| :--- | :--- |
| 72 horas | Acuse de recibo del reporte |
| 14 días | Evaluación y plan de corrección |
| 90 días | Corrección aplicada vía RFC |

## Directrices para mantenedores

- Toda corrección de seguridad DEBE tramitarse mediante RFC (26. Sistema RFC) con prioridad CRÍTICA.
- Nunca incluir secretos, tokens o claves en el repositorio (GIT-002).
- Verificar que los archivos de exclusión (GIT-001) se respetan antes de cada commit.
