# Plantilla de repositorio para AI-Agents

Esta plantilla instala los perfiles base de Copilot, las plantillas de issues y pull requests y un workflow pequeño que invoca la implementacion central de [AI-Agents](https://github.com/daniel-saezv/AI-Agents).

El motor y sus pruebas permanecen en el repositorio central: no copies `scripts/agent_loop.py`, sus pruebas ni el workflow de comprobaciones a los repositorios consumidores.

## Configuracion inicial

1. En GitHub, abre **Settings → General** de este repositorio y activa **Template repository**. Esa opcion no se puede establecer desde los archivos del repositorio.
2. Configura el acceso del repositorio central privado `AI-Agents` para permitir que este repositorio consuma sus workflows reutilizables (**Settings → Actions → General → Access** en `AI-Agents`).
3. Configura una sola vez en el workflow central `AI-Agents` los identificadores no secretos del proveedor OIDC, service account y proyecto de Google Cloud. El workflow central obtiene `COPILOT_AGENT_TOKEN` desde Secret Manager; no se requiere una clave de Google ni un secreto PAT en cada consumidor.
4. Activa Copilot cloud agent para el repositorio si tu plan lo requiere.
5. En **Settings ? Copilot ? Cloud agent** desactiva **Require approval for workflow runs**. Si no, cada cierre de etapa deja un run `action_required` y el bucle espera a que pulses *Approve and run workflows* o comentes `/agent continuar`. Opcional: desactiva **Copilot code review** en *Validation tools*, porque el agente `reviewer` ya revisa.
6. Completa la seccion **Proyecto** de `.github/copilot-instructions.md` con los comandos de build y pruebas. QA y el implementador la usan.

El workflow incluido concede `id-token: write`, necesario para que GitHub emita la identidad OIDC de corta duración. Los repositorios existentes deben actualizar su workflow invocador con ese permiso. El workflow central no acepta PATs pasados por los repositorios consumidores: obtiene el token únicamente desde Secret Manager mediante OIDC.

Si el repositorio restringe las Actions permitidas, autoriza `google-github-actions/auth` y `google-github-actions/get-secretmanager-secrets` en la politica aplicable al consumidor. El acceso para invocar el workflow privado de `AI-Agents` se habilita por separado en los Settings del repositorio central.

## Crear un repositorio desde la plantilla

En GitHub, selecciona **Use this template → Create a new repository**. La plantilla privada solo puede usarse por personas con acceso de lectura. Los repositorios creados reciben una copia con historial independiente; no son forks conectados.

El nuevo repositorio incluye:

- `.github/workflows/agent-dev-loop.yml`, que llama al workflow reutilizable central.
- `.github/agents/`, con los perfiles base `planner`, `implementer`, `reviewer` y `qa`.
- `.github/ISSUE_TEMPLATE/agent-task.yml` y `.github/PULL_REQUEST_TEMPLATE.md`.
- `.github/copilot-instructions.md`, para adaptar al proyecto.

El workflow arranca con una issue de tipo **Tarea para agentes**, con la etiqueta `agent-loop` o con `/agent empezar`. Despues avanza con el commit `Agent-Handoff` que cierra cada etapa en ramas `copilot/**`. El job filtra los eventos irrelevantes, asi que no hay ejecuciones duplicadas. Tambien se puede iniciar desde Actions indicando el numero de issue. Los detalles del protocolo estan en el README de [AI-Agents](https://github.com/daniel-saezv/AI-Agents).

## Limites

- Cambiar esta plantilla no actualiza los repositorios creados anteriormente ni mantiene sus archivos sincronizados.
- Los consumidores necesitan conservar el pequeño workflow invocador, aunque la logica del orquestador se mantenga centralizada.
- Para actualizar repositorios existentes, integra los cambios mediante pull requests o automatiza la sincronizacion por separado.
