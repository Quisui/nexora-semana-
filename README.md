# Nexora Analytics: Detección de ventas de alto valor y segmentación de clientes

Proyecto aplicado del curso CIA6041 - Inteligencia Artificial y Gestión de Datos Organizacionales, Broward International University. Caso de estudio sobre el dataset público Online Retail II (776.596 líneas de venta, 5.852 clientes, 41 países, dic. 2009 - dic. 2011).

## Integrantes

- Carlos Enrique Alvarado Legrand
- Fernando Moreno Bautista
- Silvio Bigotto Rojas

Docente: Jhony Andrés Guzmán Henao

## Pregunta de negocio

Hoy, una venta de alto valor se detecta recién después de que ya ocurrió, y todos los clientes reciben el mismo trato comercial. El proyecto responde dos preguntas concretas:

1. Cuando entra una línea de venta, ¿se puede anticipar a tiempo si es de alto valor, para que el equipo comercial la revise?
2. ¿Hay grupos de clientes con comportamientos de compra distintos que justifiquen un trato comercial diferenciado?

## Resultados: respuesta a las preguntas de negocio

### 1. ¿Se puede anticipar si una línea de venta será de alto valor?

Se define `alto_valor` como ingreso por encima de £42,07 (Q3 + 1,5×IQR), lo que marca 8,01 % de las líneas (62.197) como clase positiva. Un árbol de decisión (profundidad máxima 4), entrenado solo con `categoría`, `país`, `cantidad` y `mes` —excluyendo deliberadamente `precio_unitario` e `ingreso` por fuga de datos—, obtiene:

| Modelo | Accuracy | Precisión (alto valor) | Recall (alto valor) |
|---|---|---|---|
| Línea base (clasificador ingenuo) | 91,99 % | --- | --- |
| Árbol de decisión (producción) | 94,70 % | 80 % | 45 % |
| Control de fuga (con precio unitario) | 98,57 % | no aplica a producción | |

**Respuesta:** sí se puede anticipar, y el modelo supera la línea base en 2,70 puntos de accuracy, pero con un recall de apenas 45 % no detecta más de la mitad de las ventas de alto valor reales. **El modelo todavía no debe pasar a producción como alerta comercial automática**; antes requiere balanceo de clases, ajuste de umbral, validación temporal (entrenar en 2009-2010 y probar en 2011) y probar modelos de mayor capacidad. Debe usarse como apoyo a la decisión, nunca como automatización total.

### 2. ¿Hay grupos de clientes que justifiquen un trato comercial diferenciado?

Sí. Con RFM (Recencia, Frecuencia, Monto) y K-Means (3 segmentos, elegidos por utilidad comercial sobre una silueta de 0,402, estable frente a cambios de semilla con índice de Rand ajustado de 0,993) se identifican:

| Segmento | Clientes | Recencia (días) | Frecuencia | Monto medio |
|---|---|---|---|---|
| Alto valor | 1.675 | 57,4 | 15,8 | £8.420 |
| Activos regulares | 2.354 | 90,0 | 2,9 | £840 |
| Inactivos | 1.823 | 470,5 | 1,8 | £542 |

**Respuesta:** el segmento de alto valor gasta en promedio 10 veces más que los otros dos y debe priorizarse en cualquier programa de fidelización. El segmento inactivo lleva 470 días sin comprar en promedio y necesita una campaña de reenganche separada, sin mezclarlo con campañas activas. Los segmentos describen comportamiento histórico, no categorías permanentes del cliente.

### Limitaciones y consideraciones éticas

- La categoría de producto es aproximada (coincidencia de palabras clave) y cubre solo 40,4 % de las líneas; no debe usarse como variable determinante.
- El modelo usa el país como predictor, lo que puede asociar "alto valor" con la nacionalidad en vez del comportamiento de compra; debe monitorearse para evitar un trato comercial desigual entre países.
- La segmentación no debe comunicarse a los clientes como una categoría fija ni usarse para excluir servicio a los segmentos de menor gasto.

El detalle completo de metodología, cifras y discusión está en `informe/Nexora_Informe_Tecnico_Final.pdf`, y la exploración interactiva de estos mismos resultados en los tableros de `dashboard/`.

## Estructura de carpetas

```
nexora-analytics/
├── README.md
├── notebook/
│   └── Nexora_OnlineRetailII_Analitica.ipynb
├── data/
│   ├── Online_Retail_II_Depurado_App.xlsx      (entrada)
│   ├── OnlineRetailII_limpio.csv               (salida del ETL)
│   └── OnlineRetailII_segmentos.csv            (salida de la segmentación)
├── dashboard/
│   ├── Nexora_Tableau_Final.twbx
│   └── Online_Retail_II_Nexora_Dashboard.pbix
├── informe/
│   └── Nexora_Informe_Tecnico_Final.pdf
└── presentacion/
    ├── Nexora_Presentacion_Final.pptx
    └── Guion_presentacion_final_Nexora_6min.pdf
```

## Cómo ejecutar el proyecto

### Notebook (ETL, EDA y modelos de machine learning)

1. Colocar el archivo `Online_Retail_II_Depurado_App.xlsx` en la misma carpeta que el notebook (o ajustar la ruta en la primera celda).
2. Instalar las dependencias: `pip install pandas numpy scikit-learn matplotlib openpyxl`.
3. Abrir `notebook/Nexora_OnlineRetailII_Analitica.ipynb` en Jupyter o en Google Colab.
4. Ejecutar todas las celdas en orden (Run All / Reiniciar y ejecutar todo). El notebook exporta automáticamente `OnlineRetailII_limpio.csv` y `OnlineRetailII_segmentos.csv` en la carpeta `data/`.

### Tablero (Power BI o Tableau)

- **Power BI:** abrir `dashboard/Online_Retail_II_Nexora_Dashboard.pbix` con Power BI Desktop y actualizar el origen de datos si es necesario.
- **Tableau:** abrir `dashboard/Nexora_Tableau_Final.twbx` con Tableau Desktop o Tableau Public (el archivo ya incluye los datos empaquetados).

### Informe técnico y presentación

- El informe técnico breve está en `informe/Nexora_Informe_Tecnico_Final.pdf`.
- La presentación final y su guion están en la carpeta `presentacion/`.
