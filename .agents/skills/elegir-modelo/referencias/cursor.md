# Cursor: elegir y comprobar el modelo

Hechos para consultar. Verificado el 2026-11-21 contra la documentación oficial. Si un campo no está aquí, no lo inventes: abre el enlace.

## Documentación

- [Cloud Agents](https://cursor.com/docs/cloud-agent): selección de modelos al usar el agente en la nube.
- [Cloud Agents API](https://cursor.com/docs/cloud-agent/api/endpoints): `POST /v1/agents` (`model.id`, `model.params`) y `GET /v1/models`.
- [Cloud Agents settings](https://cursor.com/docs/cloud-agent/settings): modelo por defecto cuando una ejecución no especifica uno.
- [Agent metadata](https://cursor.com/docs/cloud-agent/metadata): modelo que sirve el turno actual (`turn/model`).
- [Capabilities](https://cursor.com/docs/cloud-agent/capabilities): el MCP Cursor Cloud (`run-info`) incluye el modelo de la ejecución actual.

## Cómo elegir

Al lanzar el cloud agent, selecciona el modelo. En la API, pásalo en el cuerpo de `POST /v1/agents`:

- `model.id`: un id que devuelva `GET /v1/models`.
- `model.params`: lista de `{ "id", "value" }`. Solo parámetros que ese modelo admite. La doc de ejemplo usa `{ "id": "fast", "value": "false" }` y, en automatizaciones, `{ "id": "reasoning", "value": "high" }`. Los valores vigentes salen de `GET /v1/models` (`parameters` y `variants`).

Si omites `model`, Cursor resuelve el modelo por defecto del usuario, luego el del equipo, luego el del sistema. Esta skill exige pasarlo siempre.

Los ids concretos (Composer 2.5, Grok 4.7 y los valores de razonamiento, incluido `xhigh` si existe) salen de `GET /v1/models` en el momento del lanzamiento. No copies un id de memoria.

## Cómo comprobar

El modelo pedido no basta. Lee el que se resolvió:

1. Dentro de la VM, durante un turno de código:

   ```bash
   curl --unix-socket "${CURSOR_AGENT_SOCKET:-/run/cursor/api.sock}" \
     http://cursor-agent/v1/meta-data/turn/model
   ```

   `turn/model` es el modelo que sirve el turno. Si elegiste Auto, es el modelo que sirvió, no `Auto`. Esta API local está en preview. En workers autoalojados aún no está.

2. Con el MCP Cursor Cloud, `run-info` de la ejecución actual incluye el modelo.

`GET /v1/agents/{id}` y `GET /v1/agents/{id}/runs/{runId}` no documentan un campo de modelo. No lo inventes.
