# Examples — Artefactos simulados

Esta carpeta contiene **artefactos de ejemplo generados durante simulaciones**, no datos de estudiantes reales del piloto. Sirven como referencia del formato esperado y como casos de prueba para auditoría del pipeline.

## Convención de naming

`<artefacto>_simulated_<persona-id>.md`

## Contenido actual

| Archivo | Generado | Persona simulada | Propósito |
|---|---|---|---|
| `student-profile_simulated_maria-fernanda.md` | 2026-05-02 | Docente de matemáticas, 8 años de experiencia, semestre 1 Maestría — perfil mixto Principiante/Intermedio | Validar el pipeline F1→F4 en modo `student` y detectar gaps pedagógicos |

## Importante

- Los artefactos del piloto real van en `quality_reports/` directamente, **no aquí**.
- Si vas a correr una simulación nueva, deja claro en el frontmatter del artefacto que es simulación y muévelo a esta carpeta cuando termines.
