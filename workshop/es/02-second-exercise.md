<!-- l10n-sync: source-file="02-second-exercise.md" -->
# Ejercicio 2 — Resumen Diario de Hacker News

En este ejercicio crearás un flujo de trabajo agéntico que automáticamente obtiene las principales historias de Hacker News relevantes para ingenieros de software profesionales y las publica como un issue diario de GitHub.

**Tiempo estimado:** 20 minutos

## Objetivos

- Escribir un prompt en lenguaje natural más rico y específico para un flujo de trabajo agéntico
- Comprender cómo el agente obtiene datos de una API externa (Hacker News)
- Inspeccionar y refinar el markdown del flujo de trabajo generado
- Validar que el issue generado sea útil y esté bien estructurado

## Contexto

La [API de Hacker News](https://hacker-news.firebaseio.com/v0/) es pública y no requiere autenticación. Expone endpoints como:

- `GET /v0/topstories.json` — devuelve hasta 500 IDs de historias principales
- `GET /v0/item/<id>.json` — devuelve los detalles de un elemento individual (historia, comentario, etc.)

Tu flujo de trabajo agéntico llamará a estos endpoints, filtrará los resultados y los formateará en un issue de GitHub legible.

## Parte 1 — Crear el Flujo de Trabajo

Crea el flujo de trabajo con `gh aw new`:

```bash
gh aw new hn-daily-digest
```

Cuando se abra la sesión interactiva del agente, proporciona la siguiente descripción:

```
Create a daily digest workflow for professional developers, referencing
relevant top Hacker News stories on technology that can be used today
by large companies. Every weekday, fetch the top 30 stories from the
Hacker News API (https://hacker-news.firebaseio.com/v0/topstories.json),
filter to stories with a score above 100 that are about software
engineering, cloud infrastructure, AI/ML, developer tooling, or
distributed systems. For each qualifying story include: the title, the
URL, the score, the number of comments, and a one-sentence summary of
why it is relevant to enterprise developers. Create a GitHub issue
titled "HN Digest – <date>" with the results formatted as a Markdown
table.
```

El agente confirmará el disparador (programación en días laborables), las herramientas requeridas (`web-fetch`, `github`), los permisos (`issues: write`), y la lista de redes permitidas (el dominio de la API de HN), y luego generará los archivos del flujo de trabajo.

> [!TIP]
> También puedes describir el flujo de trabajo en GitHub Copilot Chat escribiendo `/agent` y seleccionando **agentic-workflows** — el agente te guiará a través de una configuración conversacional.

## Parte 2 — Revisar y Refinar el Flujo de Trabajo

Abre el archivo de flujo de trabajo generado:

```bash
cat .github/workflows/hn-daily-digest.md
```

El archivo tiene dos partes:

**Frontmatter YAML** (entre marcadores `---`) — configuración que requiere recompilación:

```yaml
---
name: HN Daily Digest
on:
  schedule: daily on weekdays
  workflow_dispatch:
permissions:
  issues: write
  contents: read
network:
  - hacker-news.firebaseio.com
tools:
  - web-fetch
safe-outputs:
  create-issue:
    max: 1
---
```

**Cuerpo Markdown** (después del frontmatter) — las instrucciones en lenguaje natural que le diste al agente. Puedes editar el cuerpo directamente en GitHub.com o en cualquier editor y tus cambios tendrán efecto en la próxima ejecución, **sin necesidad de recompilar**.

> [!NOTE]
> Si deseas cambiar el disparador, las herramientas, los permisos o las reglas de red (el frontmatter), necesitas recompilar: `gh aw compile hn-daily-digest`.

### Qué Verificar

1. **Lista de redes permitidas** — ¿el frontmatter incluye `hacker-news.firebaseio.com`? El agente necesita acceso a la red para llamar a la API de HN.
2. **Programación** — ¿usa programación difusa (`daily on weekdays`) en lugar de un cron fijo? La programación difusa es preferible porque distribuye la carga y automáticamente agrega `workflow_dispatch` para ejecuciones manuales.
3. **Cuerpo del prompt** — ¿el cuerpo describe claramente los criterios de filtrado y el formato de salida deseado?

Si deseas ajustar el prompt, simplemente edita el cuerpo del markdown y el cambio tendrá efecto en la próxima ejecución. Para actualizar el frontmatter (por ejemplo, agregar un dominio de red), edita el frontmatter y recompila:

```bash
gh aw compile hn-daily-digest
```

## Parte 3 — Hacer Commit y Ejecutar el Flujo de Trabajo

Haz commit y push tanto del markdown como del archivo lock:

```bash
git add .github/workflows/hn-daily-digest.md .github/workflows/hn-daily-digest.lock.yml
git commit -m "Add HN daily digest workflow"
git push
```

Luego ejecuta una ejecución manual:

```bash
gh aw run hn-daily-digest
```

Espera a que la ejecución se complete, luego abre GitHub y revisa la pestaña **Issues**.

### Qué Verificar

- El título del issue contiene la fecha de hoy.
- El cuerpo del issue es una tabla Markdown con títulos de historias, URLs, puntuaciones y conteo de comentarios.
- Las historias son genuinamente relevantes para el desarrollo de software empresarial (no noticias generales o política).

> [!TIP]
> Si la salida se ve bien pero el formato no es correcto, edita el cuerpo markdown de `.github/workflows/hn-daily-digest.md` para agregar una plantilla de salida específica, luego haz push y vuelve a ejecutar — no se necesita recompilación.

## Criterios de Éxito

- [ ] `.github/workflows/hn-daily-digest.md` existe en tu repositorio
- [ ] `.github/workflows/hn-daily-digest.lock.yml` existe en tu repositorio
- [ ] El frontmatter del flujo de trabajo incluye `hacker-news.firebaseio.com` en la lista de redes permitidas
- [ ] El flujo de trabajo usa programación difusa (`daily on weekdays`)
- [ ] Se creó un issue de GitHub titulado **HN Digest – \<fecha de hoy\>** con una tabla Markdown de historias

---

Una vez terminado, continúa con el [Ejercicio 3: Análisis de Sentimiento ChatOps](./03-chatops-sentiment.md).
