<!-- l10n-sync: source-file="README.md" -->
# Taller de Flujos de Trabajo Agénticos

Este repositorio contiene el taller práctico de **Flujos de Trabajo Agénticos con GitHub Copilot**. Visite el sitio publicado o siga los pasos del taller en el directorio `workshop/`.

## Iniciar el taller

**Para comenzar el taller, acceda a [workshop/README.md](./workshop/README.md)**

O visite el [sitio publicado del taller](https://copilot-dev-days.github.io/agentic-workflows-workshop).

## Estructura del Repositorio

```
├── docs/           # Site HTML publicado (GitHub Pages)
│   ├── index.html  # Landing page
│   ├── step.html   # Step viewer (renders workshop/ markdown)
│   ├── styles.css
│   ├── light-theme.css
│   └── theme-toggle.js
├── workshop/       # Workshop content (markdown)
│   ├── README.md              # Workshop overview
│   ├── 00-prereqs.md          # Prerequisites & tooling
│   ├── 01-first-exercise.md   # Exercise 1 – Quick Start (gh aw init + daily digest)
│   ├── 02-second-exercise.md  # Exercise 2 – Hacker News Daily Digest
│   ├── 03-chatops-sentiment.md # Exercise 3 – ChatOps Sentiment Analysis
│   ├── 04-review.md           # Review & Next Steps
│   └── images/                # Screenshots and diagrams
├── .github/
│   ├── copilot-instructions.md
│   └── workflows/deploy.yml
├── README.md
└── LICENSE
```

## Publicación

El sitio del taller se despliega automáticamente en GitHub Pages cuando se hace push a `main`. Habilite GitHub Pages en la configuración de su repositorio (Settings → Pages → Source: GitHub Actions).

## Licencia

Este proyecto está licenciado bajo los términos de la licencia de código abierto MIT. Consulte el archivo [LICENSE](./LICENSE) para los términos completos.

## Soporte

Este proyecto se proporciona tal cual, y puede actualizarse con el tiempo. Si tiene preguntas, abra una issue.
