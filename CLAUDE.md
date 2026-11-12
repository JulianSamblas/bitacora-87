# Bitácora 87 — instrucciones de trabajo

Responder siempre en español. Feedback directo y crítico (ver `docs/proyecto.md` §8).

## Qué hay aquí

| Ruta | Qué es |
|---|---|
| `docs/proyecto.md` | Contexto completo: atleta, plan, decisiones y su porqué, evidencia, estado, pendientes. **Leer al empezar.** Es la fuente de verdad; el `proyecto.md` del Project de claude.ai es una copia. |
| `app/index.html` | Código de la app (artefacto de Claude). Es espejo del artefacto publicado. |
| `CHANGELOG.md` | Una línea por cambio, con fecha. Sustituye a releer conversaciones antiguas. |

Artefacto: slug `e91e63e7-2ef3-443d-9b10-f4bbee0c95d9` — https://claude.ai/artifact/Vncm6v5reKNxCZoecaYNXJ

## Flujo para cambiar la app (ahorra tokens)

1. No releer `app/index.html` entero: `grep -n` para localizar la zona y leer solo ese rango.
2. Editar `app/index.html` con Edit (cambios pequeños y localizados).
3. Publicar desde el fichero: `get_artifact` para la versión viva → `publish_files`
   con `{as: "index.html", path: "<repo>/app/index.html"}` y `base_version`.
   No reenviar el HTML completo con `publish_version`.
4. Si `get_artifact` da una versión distinta de la última anotada en el CHANGELOG,
   alguien editó el artefacto fuera del repo: descargarlo con `read_file` (paths) y
   comparar antes de pisarlo.
5. Commit + línea en `CHANGELOG.md` con la versión publicada.

## Flujo para cambiar el plan

Editar `docs/proyecto.md` (fecha de "Última actualización"), añadir línea al CHANGELOG,
commit, y subir la misma versión al Project con `project_write` en `proyecto.md`.

## Reglas de implementación (no romper)

- Nada de botones anidados; `<div data-act>` + un único listener delegado en `document`.
- Clonar (`clone()`) los datos de la `db` antes de modificarlos (vienen congelados).
- `input` con `font-size: 16px` (evita zoom en Safari iOS).
- Tonelaje real: peso × reps; banderas `x2`, `lado`, `nt`.
- Errores visibles en la línea de estado al pie.
- Datos en capability `db`: colecciones `days`, `tests`, `config/habits`, `config/perfil`.
  Cambiar su esquema rompe datos ya guardados: migrar, no renombrar.
