# AGENTS.md

## Reglas transversales

1. Demuestra que funciona antes de darlo por hecho: comando real, test o captura.
2. Arregla la causa raíz, no el síntoma.
3. Resta antes de sumar: borra código muerto antes de añadir.
4. Haz el cambio mínimo que resuelve, sin capas ni abstracciones especulativas.
5. Los tests prueban comportamiento observable, no la implementación.
6. Amplía un test existente antes de crear otro y borra los que dejen de aplicar.
7. Sin comentarios en el código: que el nombre y la estructura lo expliquen.
8. Validación y manejo de errores en los bordes del sistema, no repartidos por todo el código.
9. Operaciones idempotentes: se pueden repetir sin daño.
10. Una unidad verificable por commit o PR.
11. Antes de reportar un número, explícalo y mídelo bien.
12. Si una corrección se repite, conviértela en estructura (test, lint, tipo) y no en otra instrucción.
13. Nunca inventes comandos, stack ni datos: solo lo comprobado.
14. Sin ficheros `.md` largos de planes o decisiones; el porqué va en la PR o en el commit.
15. Prosa breve y sin relleno en PRs, commits y documentación.
16. No cambies alcance, diseño ni prioridades por tu cuenta; si algo te bloquea, dilo con exactitud.

## Este proyecto

Lo rellena la skill `setup-proyecto` en la primera tarea del repositorio.