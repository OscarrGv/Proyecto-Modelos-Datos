# Deserción de clientes en un banco europeo — Inferencia estadística

**Proyecto Unidad 2 · Inferencia estadística aplicada a un problema de Ciencia de Datos**

A partir de una muestra aleatoria de 1,000 clientes se estiman la deserción (*churn*) y sus características en la cartera completa de un banco europeo (10,000 clientes de Francia, Alemania y España). La incertidumbre se cuantifica con intervalos de confianza y los resultados se usan para tomar una decisión de negocio.

## Datos

**Dataset:** *Churn Modelling* (Kaggle): 10,000 clientes anonimizados de un banco con operaciones en Francia, Alemania y España. Es uno de los datasets de referencia para estudiar la deserción bancaria. Su ficha técnica, la justificación de su uso y las consideraciones de privacidad (RGPD) están en el cuaderno 01.

## Estructura

```
├── data/
│   ├── raw/Churn_Modelling.csv                ← datos ORIGINALES (10,000 clientes)
│   └── processed/
│       ├── poblacion_clientes.csv             ← población preparada, en español
│       ├── muestra_clientes_n1000.csv         ← muestra analizada
│       └── muestra_clientes_n1000.xlsx        ← misma muestra en Excel
├── notebooks/
│   ├── 00_aprende_desde_cero.ipynb            ← guía: todas las ideas explicadas desde cero, con glosario
│   ├── 01_conocer_y_preparar_datos.ipynb      ← ficha del dataset, revisión de calidad, preparación
│   ├── 02_muestreo_y_descriptiva.ipynb        ← apartados 1, 2 y 3
│   └── 03_inferencia_y_decision.ipynb         ← apartados 4 a 7 y Decisiones metodológicas
├── reports/
│   ├── Reporte_Churn_Banco_Europeo.pdf        ← documento de entrega
│   └── figures/                               ← 10 gráficas en PNG
└── requirements.txt
```

## Cómo ejecutar

```bash
pip install -r requirements.txt
```

Abre los cuadernos **en orden** (00 → 01 → 02 → 03). Si nunca has estudiado estadística, el 00 te enseña todo lo necesario con ejemplos cotidianos. Usa *Run All* y usa *Run All*. Ya vienen ejecutados, así que también se pueden leer sin correrlos. Las semillas son fijas, por lo que los resultados son reproducibles.

## Resultados principales (IC 95 %, n = 1,000 de N = 10,000)

| Parámetro | Estimación | IC 95 % | Valor real (validación) |
|---|---|---|---|
| $p$: proporción que abandona | 0.206 | (0.182, 0.230) | 0.204 ✔ |
| $\mu$: saldo promedio de quien abandona | €91,562 | (€83,665, €99,458) | €91,109 ✔ |
| $p_{inactivo} - p_{activo}$ | 0.111 | (0.063, 0.159) | 0.126 ✔ |
| $\mu_{edad,abandona} - \mu_{edad,permanece}$ | 9.4 años | (8.0, 10.8) | 7.4 ✘ |

El intervalo de la edad no atrapó el valor real. Es el tipo de fallo ocasional (≈ 1 de cada 20) que admite un 95 % de confianza, y se explica en el cuaderno 03.

**Decisión:** lanzar una campaña de retención **sólo para clientes inactivos**, empezando con un piloto con grupo de control.
