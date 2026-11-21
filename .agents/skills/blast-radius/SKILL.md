---
name: blast-radius
description: Antes de publicar un cambio, encuentra qué podría romperse en otro sitio y demuestra el hecho clave de seguridad ejecutando código real. Para «radio de explosión de X», «qué puede romper esto» o diffs pequeños que no convencen.
---

# Radio de explosión

Encuentra qué rompe un cambio en otro lugar, antes de publicarlo. Para «radio de explosión de X», «qué puede romper esto» o un diff pequeño que aún no inspira confianza.

Complementa `how`: `how` explica qué hace el código; radio de explosión, qué parte en otro sitio.

Listar llamadores no basta: una búsqueda en el árbol lo hace en segundos. El trabajo es lo que esa búsqueda no muestra.

## No confíes en tu propio informe

Un informe que suena bien no vale si no es cierto. No entregues solo el texto: localiza el uno o dos hechos de los que depende la seguridad del cambio y demuéstralos ejecutando código.

### Qué tan seguro estás

Para cada hecho del que depende que el cambio sea seguro, llévalo tan abajo en esta lista como sea barato, y di dónde te detuviste.

1. Lo afirmaste. Por sí solo no vale.
2. Señalaste la línea. `archivo:línea` real, o el fuente de la biblioteca.
3. Mostraste que el mal caso no puede ocurrir. Recorriste el fallo paso a paso y no llega.
4. Lo ejecutaste. Script o test que llama el código real y falla en voz alta si te equivocas.
5. Lo reprodujiste en la aplicación en marcha.

El paso 4 suele ser un script pequeño que importa la misma biblioteca que usa la app y llama la función que te preocupa.

## Pasos

1. **Lee el cambio.** Diff, símbolos que añade, cambia o borra, y qué hace distinto, incluido lo que el diff no dice. Pull y commits si aplica.
2. **Encuentra el hecho por el que es seguro.** Muchos cambios que parecen arriesgados lo son por un solo hecho («esta llamada solo descarta entradas de caché ya muertas»). Si se cumple, la mayoría de casos riesgosos caen. Gasta el tiempo aquí, no en una lista larga de quizás.
3. **Mira donde la búsqueda en árbol para.** Fuente de la biblioteca llamada, versión fijada y parches locales. Cuándo corre: microtareas, desmontaje, formatos en disco, otra lengua leyendo los mismos bytes, feature flags, código tres saltos después.
4. **Sé honesto con cada riesgo.** Probabilidad real y coste si ocurre. Conserva los confirmados. Lista aparte los que comprobaste y descartaste. Cita `archivo:línea` real; una búsqueda vacía también es respuesta. No inventes llamadores ni APIs.
5. **Demuestra el hecho clave.** Script o test con código real, ejecútalo y pega la salida.
6. **Cambios grandes o amplios.** Valora segunda opinión con otro modelo o revisión humana; distintos ojos detectan fallos distintos.

## Qué entregar

- **Qué hace.** Qué cambió, incluida la parte no obvia.
- **El hecho por el que es seguro.** Enuncíalo, di en qué paso quedó y muestra la prueba. Si no pudiste probarlo, marca «sin probar».
- **Riesgos.** Cómo rompe, `archivo:línea`, probabilidad e impacto, cómo comprobar. Pega prueba en los que importen.
- **Descartados.** Qué revisaste y por qué está bien.
- **Antes de fusionar.** El test o repro más barato que atrapa el fallo real, incluido el script que escribiste.

Escribe con prosa breve, cita código real y quita lo privado antes de publicar fuera del equipo.

**Respuesta:** el informe anterior, con el hecho de seguridad probado o marcado sin probar.