<!-- l10n-sync: source-file="02-second-exercise.md" -->
# Exercício 2 — Resumo Diário do Hacker News

Neste exercício, você criará um agentic workflow que automaticamente busca as principais histórias do Hacker News relevantes para engenheiros de software profissionais e as publica como uma issue diária no GitHub.

**Tempo estimado:** 20 minutos

## Objetivos

- Escrever um prompt em linguagem natural mais rico e direcionado para um agentic workflow
- Entender como o agente busca dados de uma API externa (Hacker News)
- Inspecionar e refinar o markdown do workflow gerado
- Validar que a issue de saída é útil e bem estruturada

## Contexto

A [API do Hacker News](https://hacker-news.firebaseio.com/v0/) é pública e não requer autenticação. Ela expõe endpoints como:

- `GET /v0/topstories.json` — retorna até 500 IDs das principais histórias
- `GET /v0/item/<id>.json` — retorna os detalhes de um único item (história, comentário, etc.)

Seu agentic workflow chamará esses endpoints, filtrará os resultados e os formatará em uma issue legível no GitHub.

## Parte 1 — Criar o Workflow

Crie o workflow com `gh aw new`:

```bash
gh aw new hn-daily-digest
```

Quando a sessão interativa do agente abrir, forneça a seguinte descrição:

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

O agente confirmará o gatilho (agendamento em dias úteis), ferramentas necessárias (`web-fetch`, `github`), permissões (`issues: write`) e a lista de permissão de rede (o domínio da API do HN), e então gerará os arquivos do workflow.

> [!TIP]
> Você também pode descrever o workflow no GitHub Copilot Chat digitando `/agent` e selecionando **agentic-workflows** — o agente guiará você através de uma configuração conversacional.

## Parte 2 — Revisar e Refinar o Workflow

Abra o arquivo de workflow gerado:

```bash
cat .github/workflows/hn-daily-digest.md
```

O arquivo tem duas partes:

**Frontmatter YAML** (entre os marcadores `---`) — configuração que requer recompilação:

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

**Corpo Markdown** (após o frontmatter) — as instruções em linguagem natural que você forneceu ao agente. Você pode editar o corpo diretamente no GitHub.com ou em qualquer editor, e suas alterações terão efeito na próxima execução, **sem necessidade de recompilar**.

> [!NOTE]
> Se você quiser alterar o gatilho, ferramentas, permissões ou regras de rede (o frontmatter), será necessário recompilar: `gh aw compile hn-daily-digest`.

### O Que Verificar

1. **Lista de permissão de rede** — o frontmatter inclui `hacker-news.firebaseio.com`? O agente precisa de acesso à rede para chamar a API do HN.
2. **Agendamento** — usa agendamento flexível (`daily on weekdays`) em vez de um cron fixo? O agendamento flexível é preferido porque distribui a carga e adiciona automaticamente `workflow_dispatch` para execuções manuais.
3. **Corpo do prompt** — o corpo descreve claramente os critérios de filtragem e o formato de saída desejado?

Se você quiser ajustar o prompt, simplesmente edite o corpo do markdown e a alteração terá efeito na próxima execução. Para atualizar o frontmatter (ex.: adicionar um domínio de rede), edite o frontmatter e recompile:

```bash
gh aw compile hn-daily-digest
```

## Parte 3 — Fazer Commit e Executar o Workflow

Faça commit e push tanto do markdown quanto do arquivo lock:

```bash
git add .github/workflows/hn-daily-digest.md .github/workflows/hn-daily-digest.lock.yml
git commit -m "Add HN daily digest workflow"
git push
```

Em seguida, dispare uma execução manual:

```bash
gh aw run hn-daily-digest
```

Aguarde a execução ser concluída e abra o GitHub para verificar a aba **Issues**.

### O Que Verificar

- O título da issue contém a data de hoje.
- O corpo da issue é uma tabela Markdown com títulos de histórias, URLs, pontuações e contagem de comentários.
- As histórias são genuinamente relevantes para desenvolvimento de software empresarial (não notícias gerais ou política).

> [!TIP]
> Se a saída parecer boa, mas a formatação estiver incorreta, edite o corpo do markdown de `.github/workflows/hn-daily-digest.md` para adicionar um template de saída específico, depois faça push e execute novamente — sem necessidade de recompilação.

## Critérios de Sucesso

- [ ] `.github/workflows/hn-daily-digest.md` existe no seu repositório
- [ ] `.github/workflows/hn-daily-digest.lock.yml` existe no seu repositório
- [ ] O frontmatter do workflow inclui `hacker-news.firebaseio.com` na lista de permissão de rede
- [ ] O workflow usa agendamento flexível (`daily on weekdays`)
- [ ] Uma issue no GitHub intitulada **HN Digest – \<data de hoje\>** foi criada com uma tabela Markdown de histórias

---

Quando terminar, prossiga para o [Exercício 3: Análise de Sentimento ChatOps](./03-chatops-sentiment.md).
