---
name: prove-it-works
description: Aplicar al terminar una tarea, antes de darla por cerrada. Verifica el artefacto real (ejecuta la función, lee el valor, inspecciona el diff), no un proxy ni un «compila».
---

# Demuestra que funciona

Verifica cada resultado comprobando lo real directamente: ejecuta la función, lee el valor, inspecciona el diff. No cuentan proxies (fecha de modificación, autoinformes, salida en caché, «compila»). Si un chequeo falla, sospecha del método de observación antes que del sistema.

Automatiza el chequeo cuando puedas. Un script determinista que repite la comparación vale más que una mirada puntual. Deja la salida donde la persona pueda verla y inclúyelo en el commit solo si el rastro debe ser auditable después.