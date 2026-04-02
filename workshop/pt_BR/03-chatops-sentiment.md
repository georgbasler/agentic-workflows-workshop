<!-- l10n-sync: source-file="03-chatops-sentiment.md" -->
# Exercício 3 — ChatOps: Slash Command de Análise de Sentimento

Neste exercício, você usará o **padrão ChatOps** para criar um slash command que realiza análise de sentimento nos comentários de uma história do Hacker News. Um membro da equipe cola a URL de uma história do Hacker News como comentário em uma issue do GitHub, o agente busca e analisa os comentários e, em seguida, responde diretamente na thread.

**Tempo estimado:** 20 minutos

## Objetivos

- Entender o padrão ChatOps para agentic workflows
- Criar um slash command (`/hn-sentiment`) disparado por um comentário em issue
- Fazer o agente buscar comentários do Hacker News, executar análise de sentimento e responder inline
- Testar o comando de ponta a ponta em uma issue real do GitHub

## Contexto: O Padrão ChatOps

O padrão ChatOps permite que membros da equipe disparem agentic workflows postando um **slash command** em um comentário de issue ou pull request do GitHub. O padrão funciona assim:

1. Um usuário posta um comentário contendo um slash command e argumentos (ex.: `/hn-sentiment https://news.ycombinator.com/item?id=12345`).
2. O GitHub dispara um evento webhook `issue_comment`.
3. O agentic workflow detecta o slash command, extrai os argumentos, executa sua lógica e posta o resultado como resposta na mesma thread.

Isso é poderoso porque mantém o contexto dentro do GitHub — sem necessidade de alternar para uma ferramenta separada.

Para mais detalhes, consulte a [documentação do padrão ChatOps](https://github.github.com/gh-aw/patterns/chat-ops/).

## Parte 1 — Criar o Workflow do Slash Command

Crie o workflow com `gh aw new`:

```bash
gh aw new hn-sentiment
```

Quando a sessão interativa abrir, descreva o que você deseja:

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

O agente configurará:
- **Gatilho**: `issue_comment` com uma condição que filtra comentários que começam com `/hn-sentiment`
- **Ferramentas**: `web-fetch` para chamar a API do Hacker News
- **Rede**: `hacker-news.firebaseio.com` na lista de permissão
- **Saídas seguras**: `add-comment` para responder na issue

## Parte 2 — Revisar o Workflow Gerado

Abra o arquivo gerado:

```bash
cat .github/workflows/hn-sentiment.md
```

O frontmatter terá uma aparência semelhante a:

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

Itens a verificar:

1. **Condição do gatilho** — a cláusula `if:` filtra para que o workflow só execute quando alguém digita `/hn-sentiment`, não em qualquer comentário.
2. **Lista de permissão de rede** — `hacker-news.firebaseio.com` deve estar listado para que o agente possa buscar os comentários da história.
3. **Saída segura** — `add-comment` é declarado para que o agente possa postar a análise de volta na issue.
4. **Corpo do prompt** — o corpo do markdown descreve como analisar a URL, chamar a API, classificar o sentimento e formatar a resposta.

> [!TIP]
> Você pode editar o corpo do markdown de `.github/workflows/hn-sentiment.md` diretamente (no GitHub.com ou localmente) sem recompilar. Por exemplo, você pode ajustar o template de saída ou modificar como os trechos são formatados.

## Parte 3 — Compilar, Fazer Commit e Push

Se o agente não compilou o workflow automaticamente, compile agora:

```bash
gh aw compile hn-sentiment
```

Faça commit e push tanto do markdown quanto do arquivo lock:

```bash
git add .github/workflows/hn-sentiment.md .github/workflows/hn-sentiment.lock.yml
git commit -m "Add hn-sentiment ChatOps slash command"
git push
```

> [!IMPORTANT]
> O gatilho `issue_comment` só dispara quando o arquivo lock do workflow está no **branch padrão** do repositório (geralmente `main`). Certifique-se de fazer push para `main` (ou fazer merge de um PR em `main`) antes de testar.

## Parte 4 — Testar o Slash Command

1. Abra qualquer issue no seu repositório (ou crie uma nova intitulada "Testing ChatOps").
2. Poste um comentário com uma URL real de história do Hacker News, por exemplo:

   ```
   /hn-sentiment https://news.ycombinator.com/item?id=40942509
   ```

   > [!TIP]
   > Para encontrar uma boa história para testar, abra o [Hacker News](https://news.ycombinator.com/) e escolha qualquer história que tenha mais de 50 comentários. Copie a URL da barra de endereços do navegador.

3. Aguarde de 20 a 60 segundos. O agentic workflow será executado em segundo plano.
4. Atualize a página da issue. Você deve ver um novo comentário do agente contendo:
   - Uma pontuação geral de sentimento (% Positivo / Negativo / Neutro)
   - Uma tabela ou lista dos principais trechos de comentários positivos e negativos
   - O título da história para contexto

### Exemplo de Saída Esperada

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

## Solução de Problemas

| Problema | Solução |
|----------|---------|
| O agente não responde | Verifique se o arquivo lock está no branch padrão e se a condição do gatilho está correta. |
| Erro "Item not found" | Verifique se o ID do item do Hacker News está correto e se a história não foi excluída. |
| Lista de comentários vazia | Algumas histórias ainda não têm comentários de nível superior buscados; tente uma história com mais de 50 comentários. |
| Permissão negada | Certifique-se de que `issues: write` está no frontmatter do workflow e que o arquivo lock foi recompilado. |

## Critérios de Sucesso

- [ ] `.github/workflows/hn-sentiment.md` existe e foi enviado por push para `main`
- [ ] `.github/workflows/hn-sentiment.lock.yml` existe e foi enviado por push para `main`
- [ ] Postar `/hn-sentiment <hn-url>` em uma issue do GitHub dispara o workflow
- [ ] O agente responde com uma análise detalhada de sentimento
- [ ] A resposta inclui trechos de comentários positivos e negativos

---

Quando terminar, prossiga para [Revisão e Próximos Passos](./04-review.md).
