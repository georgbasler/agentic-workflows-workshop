<!-- l10n-sync: source-file="README.md" -->
# Taller de Flujos de Trabajo Agénticos

¡Bienvenido al taller de **Agentic Workflows**! En esta sesión práctica utilizarás la capacidad de flujos de trabajo agénticos de GitHub Copilot (`gh aw`) para automatizar tareas del mundo real directamente dentro de tu repositorio de GitHub — sin servidores, sin pipelines que mantener.

## Descripción General del Taller

Los Flujos de Trabajo Agénticos te permiten describir *qué* quieres hacer en lenguaje natural. Copilot determina *cómo* hacerlo, ejecuta las herramientas necesarias y publica los resultados de vuelta en GitHub. En este taller configurarás las herramientas, construirás dos flujos de trabajo prácticos y conectarás un comando slash de ChatOps — todo desde la línea de comandos.

### Objetivos de Aprendizaje

Al finalizar este taller, serás capaz de:

1. **Configurar Agentic Workflows** — Instalar la extensión `gh aw` e inicializarla en un repositorio, y configurar un resumen diario de issues y pull requests.
2. **Construir un resumen de Hacker News** — Crear un flujo de trabajo diario que muestre historias relevantes de Hacker News como issues de GitHub.
3. **Usar el patrón ChatOps** — Implementar un comando slash que ejecute análisis de sentimiento en los comentarios de historias de Hacker News y responda en línea.

## Requisitos Previos

Antes de asistir a este taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con una suscripción activa de **Copilot Pro, Pro+, Business o Enterprise**
- [ ] **Git** instalado y configurado
- [ ] **GitHub CLI (`gh`)** instalado y autenticado (`gh auth login`)
- [ ] Comodidad básica con una terminal

> [!NOTE]
> Si estás usando Copilot Business o Copilot Enterprise, asegúrate de que el administrador de tu organización haya habilitado **Copilot Extensions** y **Agentic Workflows** en la configuración de políticas.

## Ejercicios del Taller

| Ejercicio | Tema | Duración |
|-----------|------|----------|
| [0. Requisitos Previos][ex0] | Configuración y herramientas | 10 min |
| [1. Inicio Rápido][ex1] | `gh aw init` + resumen diario de issues/PRs | 20 min |
| [2. Resumen de Hacker News][ex2] | Flujo de trabajo agéntico personalizado para historias de HN | 20 min |
| [3. Análisis de Sentimiento ChatOps][ex3] | Comando slash con el patrón ChatOps de `gh aw` | 20 min |
| [4. Revisión y Próximos Pasos][ex4] | Recapitulación y lecturas adicionales | 5 min |

## Consejos para el Éxito

1. **Sé específico en tus prompts** — cuanto más contexto proporciones, mejor rendirá el agente.
2. **Lee el archivo de flujo de trabajo generado** — entender lo que el agente escribe te ayuda a ajustarlo.
3. **Itera** — si el primer resultado no es exactamente lo que necesitas, agrega restricciones y vuelve a ejecutar.
4. **Revisa el issue/PR que crea** — los flujos de trabajo agénticos publican su salida en GitHub, así que estate atento a nuevos issues.

## Soporte

- **Durante el taller**: Levanta la mano o usa el chat para hacer preguntas.
- **Después del taller**: Abre un issue en este repositorio.

---

*¡Feliz automatización con GitHub Copilot! 🤖🚀*

[ex0]: ./00-prereqs.md
[ex1]: ./01-first-exercise.md
[ex2]: ./02-second-exercise.md
[ex3]: ./03-chatops-sentiment.md
[ex4]: ./04-review.md
