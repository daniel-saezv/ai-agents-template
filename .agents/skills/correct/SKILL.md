---
name: correct
description: Encuentra errores que los agentes repiten en este repo y haz cada uno imposible. Prioriza arquitectura, luego tipos, lint con mensaje que nombre el arreglo, tests y documentación al final. Demuestra que cada chequeo falla con un error real pasado.
---

# Correct

La persona que opera el repo corrige a los agentes una y otra vez por los mismos fallos. Cambia el repo para que el siguiente agente no pueda repetirlos.

Asume que cada contribuidor es un agente que solo ve los archivos que abrió, copia el ejemplo más cercano y toma el camino más corto que compila. Diseña el repo para que un cambio que parece correcto desde un archivo lo sea para todo el proyecto.

## Encuentra las clases de error

Lee commits recientes, reversiones, comentarios de revisión, archivos de instrucciones para agentes y comentarios que explican workarounds. Agrupa en clases. Una clase cuenta cuando ha pasado dos veces.

## Corrige cada clase al nivel más alto que funcione

1. **Elimínala con arquitectura.** Un dueño por pieza de estado y una forma soportada por tarea. Oculta internos para que el import incorrecto falle. Sustituye listas sincronizadas a mano por una fuente de verdad. Borra vías viejas y código muerto que un agente copiaría.
2. **Fuerzala con tipos para que el mal estado no se pueda escribir.** Si el mal código aún compila, añade lint o CI cuyo error nombre el archivo, tipo o función correcta. Si el patrón ya es común, falla solo cuando un cambio añade más.
3. **Prueba el comportamiento.** Arregla o borra tests que siguen pasando cuando se rompe lo que comprueban, o que fallan solo por cambiar internos.
4. **Documenta o reglas para agentes al final, solo para decisiones de criterio.** Nada falla si un agente las ignora.

## Corrige y demuestra

Arregla las clases más frecuentes ahora, un commit cada una. Demuestra que cada chequeo nuevo falla con un error pasado real. Misma orden en local y en CI. Las excepciones van en la línea ofensora con razón, fecha de caducidad y aprobación humana.

## Mantén la tabla de reglas

Conserva en el archivo de instrucciones para agentes una tabla que empareje cada regla con qué la hace cumplir. Cuando te corrijan, arregla el fallo y añade la regla. Si la regla ya existía y nada la aplica, es repetición: corrige al nivel más alto en el mismo cambio. Quita la regla cuando el fallo ya no pueda ocurrir.

**Respuesta:** cada clase con su evidencia, el nivel elegido y por qué un nivel superior no funcionó.