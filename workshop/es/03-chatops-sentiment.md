<!-- l10n-sync: source-file="03-chatops-sentiment.md" -->
# Ejercicio 3 — ChatOps: Comando Slash de Análisis de Sentimiento

En este ejercicio usarás el **patrón ChatOps** para crear un comando slash que realiza análisis de sentimiento en los comentarios de una historia de Hacker News. Un miembro del equipo pega la URL de una historia de Hacker News como comentario en un issue de GitHub, el agente obtiene y analiza los comentarios, y luego responde directamente en el hilo.

**Tiempo estimado:** 20 minutos

## Objetivos

- Comprender el patrón ChatOps para flujos de trabajo agénticos
- Crear un comando slash (`/hn-sentiment`) activado por un comentario en un issue
- Hacer que el agente obtenga comentarios de Hacker News, ejecute análisis de sentimiento y responda en línea
- Probar el comando de extremo a extremo en un issue real de GitHub

## Contexto: El Patrón ChatOps

El patrón ChatOps permite a los miembros del equipo activar flujos de trabajo agénticos publicando un **comando slash** en un comentario de un issue o pull request de GitHub. El patrón funciona así:

1. Un usuario publica un comentario que contiene un comando slash y argumentos (por ejemplo, `/hn-sentiment https://news.ycombinator.com/item?id=12345`).
2. GitHub dispara un evento webhook `issue_comment`.
3. El flujo de trabajo agéntico detecta el comando slash, extrae los argumentos, ejecuta su lógica y publica el resultado como respuesta en el mismo hilo.

Esto es poderoso porque mantiene el contexto dentro de GitHub — no es necesario cambiar a una herramienta separada.

Para más detalles, consulta la [documentación del patrón ChatOps](https://github.github.com/gh-aw/patterns/chat-ops/).

## Parte 1 — Crear el Flujo de Trabajo del Comando Slash

Crea el flujo de trabajo con `gh aw new`:

```bash
gh aw new hn-sentiment
```

Cuando se abra la sesión interactiva, describe lo que deseas:

```
Create a ChatOps slash command called /hn-sentiment. When a user posts
a comment on a GitHub issue that starts with "/hn-sentiment <url>",
where <url> is a Hacker News story URL (e.g.
https://news.ycombinator.com/item?id=12345), do the following:
1) Extract the Hacker News item ID from the URL.
2) Fetch up to 50 top-level comments for that story from the Hacker
   News API.
3) Perform sentiment analysis on the comment text, classifying each
   comment as Positive, Negative, or Neutral.
4) Produce a summary that shows: the overall sentiment (with percentage
   breakdown), the top 3 most positive comments (with excerpt), and
   the top 3 most negative comments (with excerpt).
5) Reply to the original issue comment with the analysis formatted in
   Markdown.
If no URL is provided or the URL is not a valid Hacker News item,
reply with a helpful error message.
```

El agente configurará:
- **Disparador**: `issue_comment` con una condición que filtra comentarios que comienzan con `/hn-sentiment`
- **Herramientas**: `web-fetch` para llamar a la API de Hacker News
- **Red**: `hacker-news.firebaseio.com` en la lista de permitidos
- **Salidas seguras**: `add-comment` para responder al issue

## Parte 2 — Revisar el Flujo de Trabajo Generado

Abre el archivo generado:

```bash
cat .github/workflows/hn-sentiment.md
```

El frontmatter se verá similar a:

```yaml
---
name: HN Sentiment Analysis
on:
  issue_comment:
    types: [created]
    if: startsWith(github.event.comment.body, '/hn-sentiment')
permissions:
  issues: write
  contents: read
network:
  - hacker-news.firebaseio.com
tools:
  - web-fetch
safe-outputs:
  add-comment:
    max: 1
---
```

Cosas a verificar:

1. **Condición del disparador** — la cláusula `if:` filtra para que el flujo de trabajo solo se ejecute cuando alguien escribe `/hn-sentiment`, no en cada comentario.
2. **Lista de redes permitidas** — `hacker-news.firebaseio.com` debe estar listado para que el agente pueda obtener los comentarios de la historia.
3. **Salida segura** — `add-comment` está declarado para que el agente pueda publicar el análisis de vuelta en el issue.
4. **Cuerpo del prompt** — el cuerpo del markdown describe cómo analizar la URL, llamar a la API, clasificar el sentimiento y formatear la respuesta.

> [!TIP]
> Puedes editar el cuerpo markdown de `.github/workflows/hn-sentiment.md` directamente (en GitHub.com o localmente) sin necesidad de recompilar. Por ejemplo, puedes ajustar la plantilla de salida o modificar cómo se formatean los extractos.

## Parte 3 — Compilar, Hacer Commit y Push

Si el agente no compiló el flujo de trabajo automáticamente, compílalo ahora:

```bash
gh aw compile hn-sentiment
```

Haz commit y push tanto del markdown como del archivo lock:

```bash
git add .github/workflows/hn-sentiment.md .github/workflows/hn-sentiment.lock.yml
git commit -m "Add hn-sentiment ChatOps slash command"
git push
```

> [!IMPORTANT]
> El disparador `issue_comment` solo se activa cuando el archivo lock del flujo de trabajo está en la **rama predeterminada** del repositorio (generalmente `main`). Asegúrate de hacer push a `main` (o fusionar un PR en `main`) antes de probar.

## Parte 4 — Probar el Comando Slash

1. Abre cualquier issue en tu repositorio (o crea uno nuevo titulado "Testing ChatOps").
2. Publica un comentario con una URL real de una historia de Hacker News, por ejemplo:

   ```
   /hn-sentiment https://news.ycombinator.com/item?id=40942509
   ```

   > [!TIP]
   > Para encontrar una buena historia para probar, abre [Hacker News](https://news.ycombinator.com/) y elige cualquier historia que tenga más de 50 comentarios. Copia la URL de la barra de direcciones del navegador.

3. Espera 20–60 segundos. El flujo de trabajo agéntico se ejecutará en segundo plano.
4. Actualiza la página del issue. Deberías ver un nuevo comentario del agente que contiene:
   - Una puntuación de sentimiento general (% Positivo / Negativo / Neutral)
   - Una tabla o lista de los extractos de comentarios más positivos y negativos
   - El título de la historia como contexto

### Ejemplo de Salida Esperada

```markdown
## 🔍 Hacker News Sentiment Analysis

**Story:** Why We Moved From Kubernetes to Nomad

| Sentiment | Count | Percentage |
|-----------|-------|------------|
| 😊 Positive | 23 | 46% |
| 😐 Neutral  | 18 | 36% |
| 😠 Negative |  9 | 18% |

**Overall: Mostly Positive**

### Top Positive Comments
> "This is exactly what we needed at our company — the operational simplicity of Nomad is underrated."

### Top Negative Comments
> "I don't see how this scales beyond a few hundred nodes."
```

## Solución de Problemas

| Problema | Solución |
|----------|----------|
| El agente no responde | Verifica que el archivo lock esté en la rama predeterminada y que la condición del disparador coincida. |
| Error "Item not found" | Verifica que el ID del elemento de Hacker News sea correcto y que la historia no haya sido eliminada. |
| Lista de comentarios vacía | Algunas historias aún no tienen comentarios de nivel superior obtenidos; prueba con una historia con más de 50 comentarios. |
| Permiso denegado | Asegúrate de que `issues: write` esté en el frontmatter del flujo de trabajo y que el archivo lock esté recompilado. |

## Criterios de Éxito

- [ ] `.github/workflows/hn-sentiment.md` existe y está subido a `main`
- [ ] `.github/workflows/hn-sentiment.lock.yml` existe y está subido a `main`
- [ ] Publicar `/hn-sentiment <hn-url>` en un issue de GitHub activa el flujo de trabajo
- [ ] El agente responde con un desglose de análisis de sentimiento
- [ ] La respuesta incluye extractos de comentarios positivos y negativos

---

Una vez terminado, continúa con [Revisión y Próximos Pasos](./04-review.md).
