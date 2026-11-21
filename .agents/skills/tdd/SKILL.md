---
name: tdd
description: Usar solo cuando pidan TDD, un test que falle o un test de regresión, o cuando el fallo tenga un objetivo de test local barato. Omitir si el camino de test es caro, de integración o no está claro.
---

# TDD para corrección de fallos

Cuando corrijas un fallo con un camino de test claro y barato, haz ejecutable el comportamiento roto antes de cambiar el código de producción. El objetivo es un test de regresión acotado que falle antes del arreglo y pase después.

No fuerces un test cuando sea poco práctico. Si requiere mucho harness, mocks frágiles, infraestructura lenta, estado solo de producción, pasos de reproducción vagos o mucho ruido en fixtures, omite el test nuevo y usa la verificación más cercana útil.

## Flujo

1. **Entender el fallo.** Comportamiento esperado, actual, ruta afectada y la reproducción observable más pequeña.
2. **Elegir el chequeo ejecutable más estrecho.** Prefiere el test unitario, de componente o de integración que ya use esa ruta. Si no hay camino obvio, no inventes uno solo por cumplir el flujo.
3. **Escribir primero el test que falla.** El test más pequeño que habría detectado el fallo. Codifica comportamiento esperado, no el implementation actual.
4. **Ejecutar el test nuevo antes del arreglo.** Confirma que falla por la razón correcta. Si pasa o falla por otra cosa, corrige el test o la reproducción antes de tocar la implementación.
5. **Corregir el fallo.** Cambio mínimo en producción que satisface el comportamiento esperado y preserva contratos cercanos.
6. **Reejecutar el test de regresión.** Confirma que pasa.

## Si un test que falle no es práctico

Usa el chequeo de regresión ejecutable más cercano: script acotado, comando manual de reproducción, comparación de salida, aserción en logs o chequeo de integración focalizado.

Prefiere no añadir test a un mal test. Un mal test prueba mocks, codifica detalles internos, depende de tiempo o estado global ajeno, necesita infraestructura cara para un arreglo pequeño o se borraría al día siguiente.

## Límites

- No cambies tests para que coincidan con una implementación incorrecta.
- No debilites aserciones existentes salvo que el comportamiento esperado haya cambiado de verdad y la razón quede clara.
- Mantén el test centrado en el fallo. Evita churn de fixtures o cobertura lateral.
- Si el fallo es intermitente, haz el test determinista cuando puedas y documenta la señal que fijas.
- Si el fallo revela una clase más amplia, primero el test focalizado; luego valora cobertura adicional.

## Respuesta final

Reporta evidencia, no solo el resultado:

- Nombre del test o chequeo que fallaba antes y el fallo que produjo.
- Ejecución que pasa después y validación cercana hecha.
- Si no pudiste demostrar el fallo antes, explica por qué y qué chequeo de regresión usaste en su lugar.