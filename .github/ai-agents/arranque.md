# Arranque

Solo se aplica cuando **Proyecto**, en `.github/copilot-instructions.md`, conserva marcadores `<...>`. `developer` añade estos criterios a los de la issue y se los pasa a `reviewer` y `qa`.

Usa el stack que indique la issue; si no lo indica, elige uno y justificalo en el plan.

- `BOOT1`: **Proyecto** sin marcadores, con comandos reales de preparacion, build y pruebas, y `Arrancar` con URL local y comprobacion de salud si la aplicacion puede levantarse.
- `BOOT2`: `.github/workflows/copilot-setup-steps.yml` con un unico job `copilot-setup-steps` que instala runtime y dependencias, desde el lockfile si existe, y los navegadores de Playwright si QA prueba la interfaz. Se ejecuta en `workflow_dispatch` y en `pull_request` cuando cambia ese archivo.
- `BOOT3`: un workflow de CI en `pull_request` que ejecuta los mismos comandos de build y pruebas de **Proyecto**.
- `BOOT4`: `.gitignore` adecuado al stack y lockfile versionado si el stack lo usa.
- `BOOT5`: al menos una prueba automatica y, si hay `Arrancar`, una comprobacion contra la aplicacion en marcha.
- `BOOT6`: README creado o adaptado al proyecto implementado, con proposito, requisitos, instalacion y comandos reales de ejecucion, build y pruebas segun corresponda, coherentes con **Proyecto**. Sustituye la introduccion de la plantilla, conserva la documentacion propia existente y enlaza la documentacion de AI-Agents sin duplicarla.

El setup solo se aplica a las sesiones desde la rama por defecto: en la sesion de arranque, instala lo necesario durante la propia sesion. Los workflows no contienen secretos ni permisos mayores de los necesarios.

Al revisar, comprueba ademas que **Proyecto** no conserva marcadores, que el job se llama exactamente `copilot-setup-steps` y que CI ejecuta los mismos comandos que **Proyecto**.
