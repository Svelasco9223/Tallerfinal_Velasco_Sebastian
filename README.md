# Análisis y Pronóstico del Empleo Total No Agrícola de Estados Unidos

**Trabajo final – Estadística Aplicada**
**Maestría en Ciencia de Datos – Universidad Pontificia Bolivariana**
**Autor:** Sebastián Velasco Ardila
**Fecha:** Abril 2026

---

## Descripción

Este repositorio contiene el trabajo final de la asignatura **Estadística Aplicada**, correspondiente a un análisis de series de tiempo del empleo total no agrícola de Estados Unidos (*Total Nonfarm Payroll Employment*) durante el periodo 1990-2026, con énfasis en la modelación y pronóstico mediante técnicas estadísticas clásicas y modernas.

## Pregunta de investigación

> ¿Es posible construir un modelo SARIMA que represente adecuadamente la dinámica mensual del empleo total no agrícola de Estados Unidos y genere pronósticos confiables, considerando la presencia de estacionalidad y shocks estructurales en la serie?

## Dataset

- **Fuente:** U.S. Bureau of Labor Statistics (BLS) — *Current Employment Statistics (CES)*.
- **Vía:** [FRED — Federal Reserve Bank of St. Louis](https://fred.stlouisfed.org/series/PAYNSA).
- **Series utilizadas:**
  - `PAYNSA`: All Employees, Total Nonfarm — Not Seasonally Adjusted (variable principal).
  - `PAYEMS`: All Employees, Total Nonfarm — Seasonally Adjusted (referencia comparativa).
- **Frecuencia:** Mensual.
- **Periodo cubierto:** Enero 1939 — Marzo 2026 (1.047 observaciones).
- **Ventana de modelado:** Enero 1990 — Marzo 2026 (435 observaciones).
- **Acceso:** El notebook descarga los datos directamente desde FRED en la primera celda. No requiere archivos locales.

## Estructura del proyecto
├── README.md
├── Tallerfinal_Velasco_Sebastian.ipynb    # Notebook principal con todo el análisis
├── requirements.txt                        # Dependencias de Python
├── data/
│   └── README.md                          # Información sobre la fuente de datos
└── .gitignore

## Metodología

El trabajo está organizado en cinco hitos según la guía del proyecto:

1. **Introducción al análisis de series de tiempo:** motivación, fenómeno de estudio, objetivos.
2. **Exploración de la base de datos:** análisis visual, descomposición STL, estadísticas descriptivas globales, por subperiodo y mensuales.
3. **Preparación de los datos:** validación de integridad, recorte temporal a 1990-2026, transformación logarítmica.
4. **Modelado y predicción:**
   - Pruebas de estacionariedad (ADF, KPSS).
   - Identificación de órdenes mediante ACF/PACF.
   - Ajuste y selección de SARIMA(0,1,1)(0,1,1)₁₂.
   - Diagnóstico de residuos.
   - Modelo alternativo: Prophet (Meta) con regresor COVID exógeno.
   - Pronóstico a 24 meses con ambos modelos.
5. **Evaluación:** métricas formales (MAE, RMSE, MAPE), interpretación, limitaciones y mejoras posibles.

## Hallazgos principales

| Métrica | SARIMA | Prophet | Mejora de Prophet |
|---|---|---|---|
| MAE (mil empleos) | 1.023 | 620 | −39,4% |
| RMSE (mil empleos) | 1.290 | 757 | −41,3% |
| MAPE (%) | 0,646% | 0,392% | −39,3% |
| Ancho medio IC 95% | 18.319 | 6.139 | −66,5% |

**Conclusión metodológica:** Prophet superó a SARIMA en todas las métricas de error puntual gracias al manejo explícito del shock COVID-19 mediante un regresor exógeno. SARIMA, al absorber el rebote post-COVID como dinámica regular, produjo una sobreestimación sistemática creciente en el horizonte de pronóstico. La superioridad de Prophet no se atribuye a una capacidad matemática superior, sino a la incorporación de conocimiento experto sobre eventos atípicos.

## Cómo ejecutar el notebook

### Opción 1 — Google Colab (recomendado)

1. Abrir el notebook directamente en Colab desde GitHub:
   - En GitHub, abrir el archivo `Tallerfinal_Velasco_Sebastian.ipynb`.
   - Hacer clic en el botón "Open in Colab" o reemplazar `github.com` por `colab.research.google.com/github` en la URL.
2. Ejecutar `Entorno de ejecución → Ejecutar todas`.
3. La primera celda instala Prophet automáticamente.

### Opción 2 — Local con Jupyter

```bash
# Clonar el repositorio
git clone https://github.com/Svelasco9223/Tallerfinal_Velasco_Sebastian.git
cd Tallerfinal_Velasco_Sebastian

# Crear entorno virtual (opcional pero recomendado)
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate    # Windows

# Instalar dependencias
pip install -r requirements.txt

# Abrir Jupyter
jupyter notebook Tallerfinal_Velasco_Sebastian.ipynb
```

## Dependencias

Las dependencias se instalan automáticamente con `requirements.txt`:

- pandas
- numpy
- matplotlib
- scipy
- statsmodels
- prophet

## Referencias

- Box, G. E. P., & Jenkins, G. M. (1976). *Time Series Analysis: Forecasting and Control*. Holden-Day.
- Hyndman, R. J., & Athanasopoulos, G. (2021). *Forecasting: Principles and Practice* (3rd ed.). OTexts. [https://otexts.com/fpp3/](https://otexts.com/fpp3/)
- Makridakis, S., Spiliotis, E., & Assimakopoulos, V. (2018). The M4 Competition: Results, findings, conclusion and way forward. *International Journal of Forecasting*, 34(4), 802-808.
- Taylor, S. J., & Letham, B. (2018). Forecasting at scale. *The American Statistician*, 72(1), 37-45.
- U.S. Bureau of Labor Statistics. (2026). *Current Employment Statistics — CES (National)*. [https://www.bls.gov/ces/](https://www.bls.gov/ces/)

## Licencia

Este proyecto se publica con fines académicos. Los datos provienen del dominio público de la Reserva Federal de Estados Unidos.

## Contacto

**Sebastián Velasco Ardila**
Maestría en Ciencia de Datos — Universidad Pontificia Bolivariana
GitHub: [@Svelasco9223](https://github.com/Svelasco9223)
