<!-- l10n-sync: source-file="04-review.md" -->
# Revisão e Próximos Passos

Parabéns por concluir o workshop de Agentic Workflows! 🎉🤖

## O Que Você Aprendeu

Neste workshop, você:

1. **Configurou Agentic Workflows** — Instalou o `gh aw`, executou `gh aw init` e configurou um resumo diário de issues e pull requests.
2. **Construiu um Resumo do Hacker News** — Escreveu um prompt direcionado que busca as principais histórias do HN, filtra por relevância e cria uma issue formatada no GitHub em um agendamento diário.
3. **Implementou um Slash Command ChatOps** — Usou o padrão ChatOps para criar o `/hn-sentiment`, que busca e analisa o sentimento dos comentários de histórias do Hacker News e responde inline.

## Principais Conclusões

- **Prompts são código** — O prompt que você escreve determina a qualidade do workflow gerado. Seja específico sobre fontes de dados, critérios de filtragem, formato de saída e agendamento.
- **Workflows vivem no Git** — Todos os arquivos YAML de agentic workflow ficam em `.github/agentic-workflows/` e são versionados. Revise e melhore-os como qualquer outro código.
- **ChatOps mantém o contexto no GitHub** — Slash commands disparados por comentários em issues significam que sua equipe nunca precisa sair do GitHub para executar um agente.
- **Itere rapidamente** — `gh aw run <name>` permite testar qualquer workflow instantaneamente sem esperar por um gatilho agendado.

## Continue seu Aprendizado

- 📖 [Agentic Workflows Quick Start](https://github.github.com/gh-aw/setup/quick-start/) — o guia oficial no qual este workshop é baseado
- 🔌 [ChatOps Pattern Reference](https://github.github.com/gh-aw/patterns/chat-ops/) — documentação completa do padrão de slash command
- 🤖 [GitHub Copilot Documentation](https://docs.github.com/en/copilot) — tudo sobre o Copilot
- 🌟 [Awesome Copilot](https://github.com/github/awesome-copilot) — recursos e exemplos da comunidade
- 💬 [GitHub Community Discussions](https://github.com/orgs/community/discussions) — faça perguntas e compartilhe ideias

## Ideias para Exploração Adicional

Tente expandir o que você construiu hoje:

- **Personalize o resumo do HN** — Adicione uma divisão por categorias (IA, cloud, open-source, etc.) ou um link para a principal história da semana.
- **Expanda o comando de sentimento** — Retorne uma nuvem de palavras dos termos mais comuns, ou compare o sentimento entre duas threads do HN.
- **Adicione mais slash commands** — Tente `/summarise-pr <url>` para obter um resumo de IA de um pull request postado como comentário.
- **Conecte-se a outras APIs** — Substitua o Hacker News pelo Reddit, Dev.to ou um board interno do Jira.

## Feedback

Adoraríamos ouvir seu feedback! Por favor, compartilhe suas opiniões com os facilitadores do workshop ou abra uma issue neste repositório.

---

*Obrigado por participar! Boa automação com o GitHub Copilot! 🚀*
