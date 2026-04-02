<!-- l10n-sync: source-file="03-review.md" -->
# Revisión y Próximos Pasos

¡Felicitaciones por completar el taller de Agentic Workflows! 🎉🤖

## Lo Que Aprendiste

En este taller:

1. **Configuraste Agentic Workflows** — Instalaste `gh aw`, ejecutaste `gh aw init` y configuraste un resumen diario de issues y pull requests.
2. **Construiste un Resumen de Hacker News** — Escribiste un prompt específico que obtiene las principales historias de HN, filtra por relevancia y crea un issue de GitHub formateado con una programación diaria.
3. **Implementaste un Comando Slash ChatOps** — Usaste el patrón ChatOps para crear `/hn-sentiment`, que obtiene y analiza el sentimiento de los comentarios de historias de Hacker News y responde en línea.

## Conclusiones Clave

- **Los prompts son código** — El prompt que escribes determina la calidad del flujo de trabajo generado. Sé específico sobre las fuentes de datos, los criterios de filtrado, el formato de salida y la programación.
- **Los flujos de trabajo viven en Git** — Todos los archivos YAML de flujos de trabajo agénticos viven en `.github/agentic-workflows/` y están bajo control de versiones. Revísalos y mejóralos como cualquier otro código.
- **ChatOps mantiene el contexto en GitHub** — Los comandos slash activados por comentarios en issues significan que tu equipo nunca tiene que salir de GitHub para ejecutar un agente.
- **Itera rápidamente** — `gh aw run <name>` te permite probar cualquier flujo de trabajo instantáneamente sin esperar a un disparador programado.

## Continúa Tu Aprendizaje

- 📖 [Inicio Rápido de Agentic Workflows](https://github.github.com/gh-aw/setup/quick-start/) — la guía oficial en la que se basa este taller
- 🔌 [Referencia del Patrón ChatOps](https://github.github.com/gh-aw/patterns/chat-ops/) — documentación completa para el patrón de comandos slash
- 🤖 [Documentación de GitHub Copilot](https://docs.github.com/en/copilot) — todo sobre Copilot
- 🌟 [Awesome Copilot](https://github.com/github/awesome-copilot) — recursos y ejemplos de la comunidad
- 💬 [Discusiones de la Comunidad de GitHub](https://github.com/orgs/community/discussions) — haz preguntas y comparte ideas

## Ideas para Exploración Adicional

Intenta extender lo que construiste hoy:

- **Personaliza el resumen de HN** — Agrega un desglose por categorías (IA, nube, código abierto, etc.) o enlaza a la historia principal de la semana.
- **Expande el comando de sentimiento** — Devuelve una nube de palabras de los términos más comunes, o compara el sentimiento entre dos hilos de HN.
- **Agrega más comandos slash** — Prueba `/summarise-pr <url>` para obtener un resumen de IA de un pull request publicado como comentario.
- **Conéctate a otras APIs** — Reemplaza Hacker News por Reddit, Dev.to o un tablero interno de Jira.

## Retroalimentación

¡Nos encantaría escuchar tu opinión! Por favor comparte tus comentarios con los facilitadores del taller o abre un issue en este repositorio.

---

*¡Gracias por participar! ¡Feliz automatización con GitHub Copilot! 🚀*
