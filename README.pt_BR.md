<!-- l10n-sync: source-file="README.md" -->
# Workshop de Fluxos de Trabalho Agênticos

Este repositório contém o workshop prático de **Fluxos de Trabalho Agênticos com GitHub Copilot**. Visite o site publicado ou siga os passos do workshop no diretório `workshop/`.

## Iniciar o workshop

**Para começar o workshop, acesse [workshop/README.md](./workshop/README.md)**

Ou visite o [site publicado do workshop](https://copilot-dev-days.github.io/agentic-workflows-workshop).

## Estrutura do Repositório

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

## Publicação

O site do workshop é implantado automaticamente no GitHub Pages quando você faz push para `main`. Habilite o GitHub Pages nas configurações do seu repositório (Settings → Pages → Source: GitHub Actions).

## Licença

Este projeto é licenciado sob os termos da licença de código aberto MIT. Consulte o arquivo [LICENSE](./LICENSE) para os termos completos.

## Suporte

Este projeto é fornecido como está, e pode ser atualizado ao longo do tempo. Se você tiver dúvidas, abra uma issue.
