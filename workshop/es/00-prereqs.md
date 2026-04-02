<!-- l10n-sync: source-file="00-prereqs.md" -->
# Requisitos Previos

Antes de comenzar este taller, asegúrate de tener lo siguiente configurado.

## Cuentas y Suscripciones Requeridas

- [ ] **Cuenta de GitHub** con una suscripción activa de Copilot (**Pro, Pro+, Business o Enterprise**)
- [ ] Copilot Extensions habilitado — verifica en *Settings → Copilot → Extensions* en tu cuenta de GitHub (o pregunta al administrador de tu organización)

## Herramientas Requeridas

- [ ] **Git** — [guía de instalación](https://git-scm.com/downloads)
- [ ] **GitHub CLI (`gh`)** v2.40 o posterior — [guía de instalación](https://cli.github.com/)
- [ ] **Node.js** v18 o posterior (utilizado por algunos pasos del flujo de trabajo) — [guía de instalación](https://nodejs.org/)

### Verificar GitHub CLI

```bash
gh --version
```

Deberías ver `gh version 2.x.x` o superior.

### Autenticarse con GitHub

Si aún no has autenticado la CLI, ejecuta:

```bash
gh auth login
```

Sigue las indicaciones y elige **GitHub.com** → **HTTPS** → **Login with a web browser**.

Después de iniciar sesión, verifica que funcionó:

```bash
gh auth status
```

Deberías ver `✓ Logged in to github.com`.

## Instalar la Extensión de Agentic Workflows

La extensión CLI `gh aw` se instala mediante su propio script de configuración:

```bash
curl -sL https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh | bash
```

Esto descarga e instala el binario `gh-aw` en `~/.local/share/gh/extensions/gh-aw/`.

> [!TIP]
> Para revisar el script antes de ejecutarlo, abre `https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh` en tu navegador primero.

Verifica que la extensión está disponible:

```bash
gh aw version
```

> [!TIP]
> Si `gh aw version` muestra "unknown command", verifica que GitHub CLI está instalado con `gh --version`, luego vuelve a ejecutar el script de instalación.

## Hacer Fork o Clonar Este Repositorio

Este taller utiliza un repositorio de GitHub como espacio de trabajo para todos los flujos de trabajo agénticos.

1. Haz **Fork** de este repositorio en GitHub (haz clic en **Fork** en la esquina superior derecha), o
2. **Clona** tu fork localmente:

```bash
gh repo clone <your-username>/agentic-workflows-workshop
cd agentic-workflows-workshop
```

> [!NOTE]
> Todos los comandos de `gh aw` deben ejecutarse desde dentro de un repositorio Git que esté vinculado a un remoto de GitHub. Los comandos anteriores aseguran que este sea el caso.

## Verificar Tu Configuración

Ejecuta la siguiente lista de verificación para confirmar que todo está listo:

```bash
git --version          # Should print: git version 2.x.x
gh --version           # Should print: gh version 2.x.x
gh auth status         # Should print: ✓ Logged in to github.com
gh aw version          # Should print the aw extension version
```

> [!IMPORTANT]
> Si alguna de las verificaciones falla, resuélvela antes de continuar. Pide ayuda a un facilitador si es necesario.

---

Una vez que todo esté configurado, continúa con el [Ejercicio 1: Inicio Rápido](./01-first-exercise.md).
