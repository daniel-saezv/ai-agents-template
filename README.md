# Plantilla de repositorio para AI-Agents

Esta plantilla instala los perfiles base de Copilot, las plantillas de issues y pull requests y un workflow pequeño que invoca la implementacion central de [AI-Agents](https://github.com/daniel-saezv/AI-Agents).

El motor y sus pruebas permanecen en el repositorio central: no copies `scripts/agent_loop.py`, sus pruebas ni el workflow de comprobaciones a los repositorios consumidores.

## Configuracion inicial

1. En GitHub, abre **Settings → General** de este repositorio y activa **Template repository**. Esa opcion no se puede establecer desde los archivos del repositorio.
2. Configura el acceso del repositorio central privado `AI-Agents` para permitir que este repositorio consuma sus workflows reutilizables (**Settings → Actions → General → Access** en `AI-Agents`).
3. En **Settings → Secrets and variables → Actions** de este repositorio, crea `COPILOT_AGENT_TOKEN` con un token que pueda iniciar sesiones de Copilot cloud agent y tenga acceso al repositorio.
4. Activa Copilot cloud agent para el repositorio si tu plan lo requiere.
5. Personaliza `.github/copilot-instructions.md` con las convenciones y comandos de prueba del proyecto.

## Crear un repositorio desde la plantilla

En GitHub, selecciona **Use this template → Create a new repository**. La plantilla privada solo puede usarse por personas con acceso de lectura. Los repositorios creados reciben una copia con historial independiente; no son forks conectados.

El nuevo repositorio incluye:

- `.github/workflows/agent-dev-loop.yml`, que llama al workflow reutilizable central.
- `.github/agents/`, con los perfiles base `planner`, `implementer`, `reviewer` y `qa`.
- `.github/ISSUE_TEMPLATE/agent-task.yml` y `.github/PULL_REQUEST_TEMPLATE.md`.
- `.github/copilot-instructions.md`, para adaptar al proyecto.

El workflow arranca con una issue de tipo **Tarea para agentes**, con un comentario de agente o al abrir un pull request. También se puede iniciar manualmente desde Actions indicando el numero de issue.

## Limites

- Cambiar esta plantilla no actualiza los repositorios creados anteriormente ni mantiene sus archivos sincronizados.
- Los consumidores necesitan conservar el pequeño workflow invocador, aunque la logica del orquestador se mantenga centralizada.
- Para actualizar repositorios existentes, integra los cambios mediante pull requests o automatiza la sincronizacion por separado.
