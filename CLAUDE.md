# Cómo quiero que programes

## Estilo del código
- Un método o una operación por línea. Nada encadenado ni comprimido en una sola línea.
- Usa `print` después de cada resultado importante, con una etiqueta que diga qué es:
  `print("p-valor:", p_valor)`.
- NO uses bucles `for`, comprensiones de listas, funciones propias ni clases, salvo
  que yo lo pida. Prefiero repetir una línea dos veces (una para cada grupo) a meterla
  en un bucle.
- Nombres de variables claros y en español: `media_grupo_a`, `estadistico_t`,
  `intervalo_95`.
- Cada import en su propia línea.
- Comentarios cortos que digan POR QUÉ se hace algo, no lo que ya se lee en el código.

## Orden del análisis
- Divide el análisis en pasos numerados con título. Por ejemplo: "Paso 1 · Cargar y
  revisar los datos", "Paso 2 · Plantear las hipótesis", "Paso 3 · Revisar los
  supuestos", "Paso 4 · Aplicar la prueba", "Paso 5 · Conclusión".
- Antes de cada prueba, escribe la hipótesis nula (H0), la hipótesis alternativa (H1)
  y el nivel de significancia (alfa).
- Revisa los supuestos de la prueba (normalidad, igualdad de varianzas,
  independencia, tamaño de muestra) antes de aplicarla. Si alguno no se cumple, dilo y
  propón una alternativa (por ejemplo, una prueba no paramétrica).
- Cada paso termina con una comprobación (por ejemplo, el tamaño de cada grupo o que
  no haya datos faltantes).

## Cómo reportar los resultados
- Da siempre los números reales que salieron: estadístico, p-valor, intervalo de
  confianza y tamaño del efecto cuando aplique.
- Escribe la conclusión en una frase literal: "Se rechaza H0 (p = 0.012 < 0.05): la
  media del grupo A es mayor que la del grupo B."
- Separa la significancia estadística de la importancia práctica. Si el efecto es muy
  pequeño, dilo aunque el p-valor sea bajo.
- Lenguaje literal y directo, una idea a la vez. Sin metáforas ni frases ambiguas.
- Si hay varias pruebas válidas, dime los pros y los contras y deja que yo elija.
