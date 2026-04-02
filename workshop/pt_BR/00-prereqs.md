<!-- l10n-sync: source-file="00-prereqs.md" -->
# Pré-requisitos

Antes de iniciar este workshop, certifique-se de ter o seguinte configurado.

## Contas e Assinaturas Necessárias

- [ ] **Conta GitHub** com uma assinatura ativa do Copilot (**Pro, Pro+, Business ou Enterprise**)
- [ ] Copilot Extensions habilitado — verifique em *Settings → Copilot → Extensions* na sua conta GitHub (ou peça ao administrador da sua organização)

## Ferramentas Necessárias

- [ ] **Git** — [guia de instalação](https://git-scm.com/downloads)
- [ ] **GitHub CLI (`gh`)** v2.40 ou superior — [guia de instalação](https://cli.github.com/)
- [ ] **Node.js** v18 ou superior (usado por algumas etapas do workflow) — [guia de instalação](https://nodejs.org/)

### Verifique o GitHub CLI

```bash
gh --version
```

Você deve ver `gh version 2.x.x` ou superior.

### Autentique-se no GitHub

Se você ainda não autenticou o CLI, execute:

```bash
gh auth login
```

Siga as instruções e escolha **GitHub.com** → **HTTPS** → **Login with a web browser**.

Após fazer login, verifique se funcionou:

```bash
gh auth status
```

Você deve ver `✓ Logged in to github.com`.

## Instale a Extensão Agentic Workflows

A extensão CLI `gh aw` é instalada através do seu próprio script de configuração:

```bash
curl -sL https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh | bash
```

Isso baixa e instala o binário `gh-aw` em `~/.local/share/gh/extensions/gh-aw/`.

> [!TIP]
> Para revisar o script antes de executá-lo, abra `https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh` no seu navegador primeiro.

Verifique se a extensão está disponível:

```bash
gh aw version
```

> [!TIP]
> Se `gh aw version` mostrar "unknown command", verifique se o GitHub CLI está instalado com `gh --version` e depois execute o script de instalação novamente.

## Faça Fork ou Clone deste Repositório

Este workshop usa um repositório GitHub como espaço de trabalho para todos os agentic workflows.

1. Faça **Fork** deste repositório no GitHub (clique em **Fork** no canto superior direito), ou
2. **Clone** o seu fork localmente:

```bash
gh repo clone <your-username>/agentic-workflows-workshop
cd agentic-workflows-workshop
```

> [!NOTE]
> Todos os comandos `gh aw` devem ser executados de dentro de um repositório Git que esteja vinculado a um remote do GitHub. Os comandos acima garantem que esse seja o caso.

## Verifique sua Configuração

Execute o checklist a seguir para confirmar que tudo está pronto:

```bash
git --version          # Should print: git version 2.x.x
gh --version           # Should print: gh version 2.x.x
gh auth status         # Should print: ✓ Logged in to github.com
gh aw version          # Should print the aw extension version
```

> [!IMPORTANT]
> Se alguma das verificações falhar, resolva-a antes de prosseguir. Peça ajuda a um facilitador se necessário.

---

Quando tudo estiver configurado, prossiga para o [Exercício 1: Início Rápido](./01-first-exercise.md).
