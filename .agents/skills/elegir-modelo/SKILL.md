---
name: elegir-modelo
description: Elige y comprueba el modelo de un agente en la nube. Pasa el modelo de forma explícita y justifica plataforma y modelo en el informe o la PR.
---

# Elegir modelo

Usa esta skill al lanzar un agente en la nube.

Los detalles de cada plataforma (cómo pasar el modelo, cómo comprobarlo, catálogo) están en [referencias/cursor.md](referencias/cursor.md) y [referencias/copilot.md](referencias/copilot.md). No los copies a `AGENTS.md`.

## Qué hacer

1. **Elige plataforma y modelo juntos.** Mira la tarea. Aplica las reglas de política de abajo. Justifica ambos en el informe o la PR.
2. **Pasa el modelo de forma explícita.** Nunca dejes el de por defecto. Sigue la referencia de la plataforma: id, parámetros y el canal con el que lanzas.
3. **Comprueba el modelo que se resolvió realmente.** No asumas que el id pedido es el usado. Lee el dato que documenta la referencia.
4. **Aplica las reglas de política.** Si el modelo resuelto no coincide con lo justificado, para y relanza.

## Reglas de política

- En Cursor, solo modelos Grok o Composer, y siempre con `fast=false`. Grok 4.7 con razonamiento high o xhigh para depuración difícil, fallos intermitentes, spikes de investigación y refactors grandes. Composer 2.5 para cambios pequeños y mecánicos.
- Si la tarea necesita Claude, GPT, Gemini o MAI Code, va por Copilot.
- Plataforma y modelo se justifican en cada tarea.

## Qué no hacer

- No dejes el modelo por defecto de la cuenta, el equipo o el sistema.
- No nombres una plataforma como obligatoria en `AGENTS.md`.
