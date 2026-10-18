# Arranque

Solo se aplica cuando **Proyecto**, en `.github/copilot-instructions.md`, conserva marcadores `<...>`. `developer` añade estos criterios a los de la issue, con su tipo, y se los pasa a `reviewer` y `qa`.

Usa el stack que indique la issue; si no lo indica, elige uno y justificalo en el plan.

- `BOOT1` [QA]: **Proyecto** sin marcadores, con comandos reales de preparacion, build y pruebas, y `Arrancar` con URL local y comprobacion de salud si la aplicacion puede levantarse. Los comandos funcionan tal como estan escritos en la sesion: las variables que necesiten tienen valores por defecto en el proyecto o las define el setup.
- `BOOT2` [revision]: `.github/workflows/copilot-setup-steps.yml` con un unico job `copilot-setup-steps` con `timeout-minutes: 59`, que limita toda la sesion del agente, y que instala runtime y dependencias, desde el lockfile si existe, y los navegadores de Playwright si QA prueba la interfaz. Se ejecuta en `workflow_dispatch` y en `pull_request` cuando cambia ese archivo.
- `BOOT3` [revision]: un workflow de CI en `pull_request` que ejecuta los mismos comandos de build y pruebas de **Proyecto**, con `concurrency` por pull request y `cancel-in-progress: true`.
- `BOOT4` [revision]: `.gitignore` adecuado al stack y lockfile versionado si el stack lo usa.
- `BOOT5` [QA]: al menos una prueba automatica y, si hay `Arrancar`, una comprobacion contra la aplicacion en marcha. Si hay interfaz web, las pruebas de navegador usan `@playwright/test` del proyecto, que QA tambien usa.
- `BOOT6` [revision]: README creado o adaptado al proyecto implementado, con proposito, requisitos, instalacion y comandos reales de ejecucion, build y pruebas segun corresponda, coherentes con **Proyecto**. Sustituye la introduccion de la plantilla, conserva la documentacion propia existente y enlaza la documentacion de AI-Agents sin duplicarla.

El setup solo se aplica a las sesiones desde la rama por defecto: en la sesion de arranque, instala lo necesario durante la propia sesion y prepara los servicios con las mismas credenciales y variables que setup y CI. La red de la sesion esta limitada por el firewall: los paquetes del sistema no se descargan, asi que instala los navegadores con `npx playwright install chromium`, sin `--with-deps`; el setup y la CI si pueden usarlo. Los workflows no contienen secretos ni permisos mayores de los necesarios.

Al revisar, comprueba ademas que **Proyecto** no conserva marcadores, que el job se llama exactamente `copilot-setup-steps` con `timeout-minutes: 59` y que CI ejecuta los mismos comandos que **Proyecto**.
