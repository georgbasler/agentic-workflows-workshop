<!-- l10n-sync: source-file="README.md" -->
# Workshop de Agentic Workflows

Bem-vindo(a) ao workshop de **Agentic Workflows**! Nesta sessão prática, você usará a capacidade de fluxos de trabalho agênticos do GitHub Copilot (`gh aw`) para automatizar tarefas do mundo real diretamente no seu repositório GitHub — sem servidores, sem pipelines para manter.

## Visão Geral do Workshop

Agentic Workflows permitem que você descreva *o que* deseja fazer em linguagem natural. O Copilot descobre *como* fazer, executa as ferramentas necessárias e publica os resultados de volta no GitHub. Neste workshop, você configurará as ferramentas, construirá dois fluxos de trabalho práticos e criará um comando ChatOps — tudo pela linha de comando.

### Objetivos de Aprendizagem

Ao final deste workshop, você será capaz de:

1. **Configurar Agentic Workflows** — Instalar a extensão `gh aw`, inicializá-la em um repositório e configurar um resumo diário de issues e pull requests.
2. **Criar um resumo do Hacker News** — Criar um fluxo de trabalho diário que destaca histórias relevantes do Hacker News como issues no GitHub.
3. **Usar o padrão ChatOps** — Implementar um slash command que executa análise de sentimento nos comentários de histórias do Hacker News e responde inline.

## Pré-requisitos

Antes de participar deste workshop, certifique-se de que você possui:

- [ ] Uma conta GitHub com uma assinatura ativa do **Copilot Pro, Pro+, Business ou Enterprise**
- [ ] **Git** instalado e configurado
- [ ] **GitHub CLI (`gh`)** instalado e autenticado (`gh auth login`)
- [ ] Conforto básico com o terminal

> [!NOTE]
> Se você está usando Copilot Business ou Copilot Enterprise, certifique-se de que o administrador da sua organização habilitou **Copilot Extensions** e **Agentic Workflows** nas configurações de política.

## Exercícios do Workshop

| Exercício | Tópico | Duração |
|-----------|--------|---------|
| [0. Pré-requisitos][ex0] | Configuração e ferramentas | 10 min |
| [1. Início Rápido][ex1] | `gh aw init` + resumo diário de issues/PRs | 20 min |
| [2. Resumo do Hacker News][ex2] | Fluxo de trabalho agêntico personalizado para histórias do HN | 20 min |
| [3. Análise de Sentimento ChatOps][ex3] | Slash command com o padrão ChatOps do `gh aw` | 20 min |
| [4. Revisão e Próximos Passos][ex4] | Recapitulação e leitura complementar | 5 min |

## Dicas para o Sucesso

1. **Seja específico nos seus prompts** — quanto mais contexto você fornecer, melhor o agente se comporta.
2. **Leia o arquivo de workflow gerado** — entender o que o agente escreveu ajuda a ajustá-lo.
3. **Itere** — se o primeiro resultado não estiver perfeito, adicione restrições e execute novamente.
4. **Verifique a issue/PR criada** — agentic workflows publicam seus resultados no GitHub, então fique atento a novas issues.

## Suporte

- **Durante o workshop**: Levante a mão ou use o chat para fazer perguntas.
- **Após o workshop**: Abra uma issue neste repositório.

---

*Boa automação com o GitHub Copilot! 🤖🚀*

[ex0]: ./00-prereqs.md
[ex1]: ./01-first-exercise.md
[ex2]: ./02-second-exercise.md
[ex3]: ./03-chatops-sentiment.md
[ex4]: ./04-review.md
