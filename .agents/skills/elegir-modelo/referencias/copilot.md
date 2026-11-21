# Copilot: elegir y comprobar el modelo

Hechos para consultar. Catálogo oficial verificado el 2026-11-21. Ids y fallos de resolución, comprobados el mismo día en el log `Running Copilot cloud agent`. Si un campo no está aquí, no lo inventes: abre el enlace.

## Documentación

- Catálogo vigente: [Changing the AI model for GitHub Copilot cloud agent](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/changing-the-ai-model)
- Cómo pasar el modelo al asignar una issue: [Using Copilot cloud agent via the API](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/use-cloud-agent-via-the-api)
- Esquema de tareas (campo `model` en cada sesión): [REST API endpoints for agent tasks](https://docs.github.com/en/rest/agent-tasks/agent-tasks?apiVersion=2026-03-10) (`GET /agents/tasks/{task_id}`, versión `2026-03-10`)

## Cómo elegir

En los puntos de entrada con selector (issue en GitHub.com, comentario `@copilot` en una PR, pestaña o panel de agentes, GitHub Mobile, Raycast, Slack o Teams), elige el modelo al arrancar. Si el modelo admite razonamiento configurable, la UI muestra un segundo menú. Donde no hay selector, Copilot usa Auto.

Por API, pasa el modelo de forma explícita. Sin `model`, Copilot usa Auto.

**REST (issues):** cabecera `X-GitHub-Api-Version: 2022-11-28`. Cuerpo con `assignees: ["copilot-swe-agent[bot]"]` y `agent_assignment.model`. Endpoints: `POST /repos/{owner}/{repo}/issues`, `POST /repos/{owner}/{repo}/issues/{n}/assignees`, `PATCH /repos/{owner}/{repo}/issues/{n}`.

**GraphQL:** `agentAssignment.model` con cabecera `GraphQL-Features: coding_agent_model_selection`.

**REST (tareas):** `POST /agents/repos/{owner}/{repo}/tasks` con `model`. Si omites `model`, Auto.

Los valores son identificadores en minúsculas. La lista «Currently supported values» de las tareas REST puede ir desfasada respecto al catálogo de «Changing the AI model». Antes de elegir, abre esa página.

Ids resueltos el 2026-11-21 en `[cca-engine] Model resolution: … → resolved="<id>"`:

- `claude-haiku-4.5`
- `grok-4.7`
- `gpt-6.2-sol`
- `gpt-6.1-sol`

Sin nivel de razonamiento se usa medium. Los niveles altos gastan más créditos (la doc oficial lo confirma).

## Cómo comprobar

Un modelo inválido o no disponible no falla el HTTP de creación de la issue: responde **201**. Copilot comenta que el modelo no está disponible y no abre sesión ni PR. Revisa siempre los comentarios de la issue tras asignar.

El modelo realmente usado:

1. Log del workflow **Running Copilot cloud agent** (`GET /repos/{owner}/{repo}/actions/runs/{id}/logs`). Línea `[cca-engine] Model resolution: … → resolved="<id>"`.
2. Campo `model` de las sesiones en `GET /agents/tasks/{task_id}` (API `2026-03-10`), con permiso de repositorio **Agent tasks**. No figura en la PR.

No des por bueno el id pedido hasta ver comentarios y log.
