# Plantilla para proyectos con agentes

Punto de partida para repositorios nuevos que trabajen con Cursor o GitHub Copilot. Crea el tuyo con **Use this template** en GitHub.

## Primer paso

Pide al agente que ejecute la skill **setup-proyecto**. Esa skill explora el repositorio, rellena la sección «Este proyecto» en `AGENTS.md`, sustituye este README y propone CI y Dependabot según el stack real.

## Qué incluye

- `AGENTS.md`: reglas transversales y, tras el setup, datos del proyecto (stack, estructura, comandos comprobados).
- `.agents/skills/`: ocho skills reutilizables (setup, PR, TDD, escritura técnica, exploración, radio de explosión, verificación y corrección estructural).
- `.github/copilot-instructions.md`: enlace simbólico a `AGENTS.md` para que Copilot lea las mismas reglas.
- Plantilla de pull request y Dependabot para GitHub Actions.

`AGENTS.md` y `.agents/skills/` son la única fuente de instrucciones para agentes en Cursor y Copilot.

## Windows y enlaces simbólicos

Sin `core.symlinks=true`, Git en Windows guarda `.github/copilot-instructions.md` como archivo de texto en lugar de enlace. Actívalo:

```bash
git config --global core.symlinks true
```

Vuelve a clonar el repositorio después de cambiar la opción.

## Créditos

Las skills `prove-it-works`, `tdd`, `technical-writing`, `how`, `blast-radius` y `correct` son adaptaciones en español del proyecto [pstack](https://github.com/cursor/plugins/tree/main/pstack) de Lauren Tan (licencia MIT). Ver `.agents/skills/LICENSE`.