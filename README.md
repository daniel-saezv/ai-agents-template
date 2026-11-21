# Plantilla para proyectos con agentes

Punto de partida para repositorios nuevos que trabajen con Cursor, GitHub Copilot, Codex, Gemini CLI o Claude Code. Crea el tuyo con **Use this template** en GitHub.

## Primer paso

Pide al agente que ejecute la skill **setup-proyecto**. Esa skill explora el repositorio, rellena la sección «Este proyecto» en `AGENTS.md`, sustituye este README y propone CI y Dependabot según el stack real.

## Qué incluye

- `AGENTS.md`: reglas transversales y, tras el setup, datos del proyecto (stack, estructura, comandos comprobados).
- `.agents/skills/`: skills del agente (ver más abajo).
- `skills-lock.json`: versiones fijadas de las skills instaladas desde pstack.
- `.claude/skills/`: enlaces simbólicos para Claude Code hacia `.agents/skills/`.
- `.github/copilot-instructions.md`: enlace simbólico a `AGENTS.md` para que Copilot lea las mismas reglas.
- Plantilla de pull request y Dependabot para GitHub Actions.

`AGENTS.md` y `.agents/skills/` son la fuente de instrucciones para agentes en Cursor, Copilot, Codex y Gemini CLI. Claude Code lee las mismas skills vía `.claude/skills/`.

## Skills

Hay dos clases:

1. **Instaladas desde pstack** (inglés, instalador oficial): `blast-radius`, `correct`, `principle-prove-it-works`, `tdd` y `unslop`. Se añaden o actualizan con el CLI [`skills`](https://github.com/vercel-labs/skills), por ejemplo:

   ```bash
   npx skills add cursor/plugins --skill tdd -a cursor -a github-copilot -a codex -a gemini-cli -a claude-code -y
   ```

   Esas skills pueden nombrar otras de pstack que no vienen en la plantilla (por ejemplo, `blast-radius` menciona `why` y `arena`). Si las necesitas, instálalas con `npx skills add cursor/plugins --skill <nombre>` o con `/add-plugin pstack` en Cursor.

2. **Propias de la plantilla** (español): `setup-proyecto`, `pr-lista`, `technical-writing` y `how`. Viven solo en este repositorio; para que Claude Code las vea, mantén los enlaces en `.claude/skills/` apuntando a `.agents/skills/<nombre>`.

Para actualizar las skills bloqueadas en `skills-lock.json`:

```bash
npx skills update -y
```

Revisa el diff, valida con `npx skills check` y commitea `.agents/skills/`, `.claude/skills/` y `skills-lock.json`.

## Windows y enlaces simbólicos

Sin `core.symlinks=true`, Git en Windows guarda `.github/copilot-instructions.md` y `.claude/skills/*` como archivos de texto en lugar de enlaces. Actívalo:

```bash
git config --global core.symlinks true
```

Vuelve a clonar el repositorio después de cambiar la opción.

## Créditos

Skills de [pstack](https://github.com/cursor/plugins/tree/main/pstack) por Lauren Tan (licencia MIT), instaladas con el instalador oficial. Las adaptaciones en español `how` y `technical-writing` derivan del mismo origen; ver `.agents/skills/LICENSE`.