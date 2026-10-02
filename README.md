# Nexora Analytics: Detección de ventas de alto valor y segmentación de clientes

Proyecto aplicado del curso CIA6041 - Inteligencia Artificial y Gestión de Datos Organizacionales, Broward International University. Caso de estudio sobre el dataset público Online Retail II.

## Integrantes

- Carlos Enrique Alvarado Legrand
- Fernando Moreno Bautista
- Silvio Bigotto Rojas

Docente: Jhony Andrés Guzmán Henao

## Pregunta de negocio

Hoy, una venta de alto valor se detecta recién después de que ya ocurrió, y todos los clientes reciben el mismo trato comercial. El proyecto responde dos preguntas concretas:

1. Cuando entra una línea de venta, ¿se puede anticipar a tiempo si es de alto valor, para que el equipo comercial la revise?
2. ¿Hay grupos de clientes con comportamientos de compra distintos que justifiquen un trato comercial diferenciado?

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
