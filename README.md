# Deserción de clientes en un banco europeo · Inferencia estadística

**Proyecto Unidad 2 · Inferencia estadística aplicada a un problema de Ciencia de Datos**

El banco tiene **10,000 clientes** en Francia, Alemania y España. Sorteamos **1,000** y, con esa muestra, estimamos cuántos clientes abandonan el banco, cuánto dinero se llevan y quiénes abandonan más. Al final usamos los resultados para decidir a quién dirigir una campaña de retención.

**Cómo usar este repositorio:**

1. Lee el reporte PDF completo una vez.
2. Abre el cuaderno de estudio (`clases/cuaderno_de_estudio_inferencia.ipynb`): sigue el reporte sección por sección (1 a 8 y Conclusiones), con los números, las frases para la exposición y las preguntas probables del profesor.
3. Revisa los cuadernos 01, 02 y 03 con el PDF abierto al lado, siguiendo la tabla «Del reporte a los cuadernos».
4. Si una idea no queda clara, búscala en el cuaderno 00 o en su glosario.

---

## Qué hay en cada carpeta

| Archivo | Qué es | ¿Se entrega? |
|---|---|---|
| `data/raw/Churn_Modelling.csv` | Datos originales de Kaggle (10,000 clientes) | Sí (Anexo A) |
| `data/processed/poblacion_clientes.csv` | Población preparada, en español | Sí (Anexo A) |
| `data/processed/muestra_clientes_n1000.csv` y `.xlsx` | La muestra de 1,000 clientes | Sí (Anexo A) |
| `notebooks/00_aprende_desde_cero.ipynb` | Todas las ideas explicadas desde cero, con glosario | Sí (Anexo B) |
| `notebooks/01_conocer_y_preparar_datos.ipynb` | Ficha del dataset, revisión de calidad, preparación | Sí (Anexo B) |
| `notebooks/02_muestreo_y_descriptiva.ipynb` | Secciones 1, 2 y 3 del reporte | Sí (Anexo B) |
| `notebooks/03_inferencia_y_decision.ipynb` | Secciones 4 a 8 y Conclusiones del reporte | Sí (Anexo B) |
| `reports/Reporte_Churn_Banco_Europeo.pdf` | Documento de entrega | Sí |
| `reports/figures/` | Las 10 gráficas del reporte en PNG | Sí |
| `clases/cuaderno_de_estudio_inferencia.ipynb` | Cuaderno para estudiar y preparar la exposición | **No** (sólo para el equipo) |

---

## Las cuatro preguntas del proyecto

| Pregunta | Qué se quiere conocer | Parámetro | Técnica |
|---|---|---|---|
| P1 | Qué proporción de clientes abandona el banco | $p$ | Intervalo para una proporción |
| P2 | Saldo promedio de los clientes que abandonan | $\mu$ | Intervalo para una media (t de Student) |
| P3 | Cuánto más abandonan los inactivos que los activos | $p_1 - p_2$ | Intervalo para una diferencia de proporciones |
| P4 | Cuántos años más tienen quienes abandonan | $\mu_1 - \mu_2$ | Intervalo para una diferencia de medias (Welch) |

**Cómo se conectan con la decisión:** P1 y P3 dicen en qué grupo hay suficiente abandono para que la campaña gane dinero. P2 dice cuánto dinero se pierde por cada cliente que se va. P4 describe el perfil de quien se va.

---

## Resultados (IC 95 %, n = 1,000 de N = 10,000)

| Pregunta | Estimación puntual | IC 95 % | Valor real (comprobación) | ¿Acertó? |
|---|---|---|---|---|
| P1 · proporción que abandona | 0.206 | (0.182, 0.230) | 0.204 | Sí |
| P2 · saldo promedio de quien abandona | 91,562 € | (83,665 €; 99,458 €) | 91,109 € | Sí |
| P3 · inactivos − activos | 0.111 | (0.063, 0.159) | 0.126 | Sí |
| P4 · edad abandona − edad se queda | 9.4 años | (8.0, 10.8) | 7.4 años | No |

**De dónde sale cada número:** todos se calculan en el cuaderno 03, sólo con la muestra. Los valores reales se calculan con los 10,000 clientes **después** de estimar, y sólo para comprobar.

### Conclusión de cada pregunta

- **P1.** Con 95 % de confianza, entre el 18.2 % y el 23.0 % de los clientes abandona el banco: entre 1,822 y 2,298 de los 10,000.
- **P2.** Con 95 % de confianza, el saldo promedio de los clientes que abandonan está entre 83,665 € y 99,458 €.
- **P3.** Con 95 % de confianza, los inactivos abandonan entre 6.3 y 15.9 puntos porcentuales más que los activos. El intervalo no contiene el 0. Los inactivos abandonan 1.72 veces más (riesgo relativo). Es una asociación, no una causa.
- **P4.** Con 95 % de confianza, quienes abandonan son entre 8.0 y 10.8 años mayores. El intervalo no contiene el 0 y el efecto es grande (d de Cohen = 0.96). El valor real (7.4 años) quedó fuera del intervalo.

### Comprobación del método

| Comprobación | Resultado | Qué significa |
|---|---|---|
| Intervalos del estudio que contienen el valor real | 3 de 4 | Falló P4. Con 95 % de confianza se espera que falle cerca de 1 de cada 20 intervalos |
| Simulación: 1,000 intervalos para P1 | 946 contienen la $p$ real (94.6 %) | El método acierta cerca de 95 de cada 100 veces |

---

## La decisión

**Pregunta:** si fuéramos el área de retención del banco, ¿a quién dirigiríamos una campaña (llamada de un asesor más una bonificación)?

| Opción | Descripción |
|---|---|
| A1 | No hacer campaña |
| A2 | Campaña sólo a clientes inactivos |
| A3 | Campaña a todos los clientes |

**Supuestos** (no vienen de los datos): costo por cliente $c$ = 25 €, efectividad $e$ = 25 %, valor de un cliente retenido $V$ = 500 € al año.

**Umbral:** la campaña gana dinero si la tasa de abandono del grupo supera

$$p^* = \frac{c}{e \cdot V} = \frac{25}{0.25 \times 500} = 0.20$$

| Grupo | IC 95 % de su tasa de abandono | Comparación con 0.20 | Decisión |
|---|---|---|---|
| Inactivos | (0.227, 0.304) | Todo el intervalo está por encima | La campaña conviene |
| Activos | (0.126, 0.184) | Todo el intervalo está por debajo | La campaña no conviene |

| Criterio | Resultado | Opción elegida |
|---|---|---|
| Valor esperado | A2 gana 38,000 € | A2 |
| Mejor peor caso (maximin) | A2: 15,910 €; A1: 0 €; A3: −34,061 € | A2 |
| Mínimo arrepentimiento | A2: 0 € | A2 |
| Sensibilidad | A2 gana en todo el intervalo si la efectividad es de al menos 22 % | El supuesto (25 %) está 3 puntos por encima |
| Dinero en juego | Los clientes que abandonan se llevan entre 152 y 229 millones de € | No actuar es el error más caro |

**Recomendación:**

1. Lanzar la campaña de retención sólo a clientes inactivos.
2. No gastar presupuesto en los clientes activos.
3. Empezar con un piloto con grupo de control (500 inactivos con campaña y 500 sin ella, sorteados) para medir la efectividad real.
4. Investigar el mayor abandono en Alemania (cerca de 28 % contra 18 % en Francia y España).

---

## Del reporte a los cuadernos

Los cuadernos 02 y 03 usan **los mismos números de sección que el reporte**. Cada sección tiene una nota **📄 En el reporte PDF** con su sección, tabla o gráfica. Cada celda de código empieza con `# QUÉ HACE ESTA CELDA:` y cada instrucción tiene un comentario que dice qué hace.

| Sección del reporte PDF | Cuaderno | Dónde | Cuaderno de estudio |
|---|---|---|---|
| Introducción y «Las ideas clave» (Tabla 0) | 00 | Todo el cuaderno | Portada |
| Ficha técnica del dataset (Tabla 1) | 01 | Paso 1 | — |
| 1. Planteamiento del problema (Tabla 2) | 02 | Sección 1 | Sección 1 |
| 2.1 Población y calidad de los datos | 01 | Pasos 3 y 4 | Sección 2 |
| 2.2 ¿Por qué una muestra? | 02 | Sección 2.2 | Sección 2 |
| 2.3 Tamaño de la muestra (Tabla 3) | 02 | Sección 2.3 | Sección 2 |
| 2.4 Método, criterios y representatividad (Tabla 4) | 02 | Sección 2.4 | Sección 2 |
| 3. Recolección y descripción (Tablas 5–7, Gráficas 1–5) | 02 | Sección 3 | Sección 3 |
| 4. Estimación puntual (Tabla 8) | 03 | Sección 4 | Sección 4 |
| 5. Estimación por intervalo, 5.1–5.4 (Tabla 9, Gráfica 6) | 03 | Secciones 5.1 a 5.4 | Sección 5 |
| 6.1 ¿Qué significa cada intervalo? | 03 | Sección 6.1 | Sección 6 |
| 6.2 Nivel de confianza (Gráfica 7) | 03 | Sección 6.2 | Sección 6 |
| 6.3 Tamaño de muestra (Gráfica 8) | 03 | Sección 6.3 | Sección 6 |
| 6.4 Comprobación con la población (Gráfica 9) | 03 | Sección 6.4 | Sección 6 |
| 6.5 Limitaciones | 03 | Sección 6.5 | Sección 6 |
| 7. Teoría de decisión (Tablas 10–11, Gráfica 10) | 03 | Secciones 7.1 a 7.7 | Sección 7 |
| 8. Decisiones metodológicas | 03 | Sección 8 | Sección 8 |
| Conclusiones | 03 | Conclusiones | Conclusiones y guion |
| Anexo C. Glosario | 00 | Glosario rápido | — |

**Dos números del reporte PDF no coinciden con los cuadernos:**

| Dato | Reporte PDF | Cuadernos | Por qué |
|---|---|---|---|
| Cobertura de la simulación (6.4) | 94.2 % | 94.6 % | La simulación se reprogramó con otro sorteo |
| Límite inferior de los inactivos (Tabla 10) | 0.228 | 0.227 | El valor exacto es 0.22749 |

Hay que corregir el PDF antes de entregar o explicar la diferencia en la exposición.

---

## Cómo ejecutar

```bash
pip install -r requirements.txt
```

1. Abre los cuadernos en orden: 00 → 01 → 02 → 03.
2. En cada uno usa *Run All*.
3. Ya vienen ejecutados: también se pueden leer sin correrlos.
4. Las semillas son fijas (2026 para la muestra), así que los resultados salen iguales cada vez.

**Comprobación:** al correr el cuaderno 03 debe salir «Intervalos que contienen el valor real: 3 de 4» y «Intervalos que contienen a p: 946».
