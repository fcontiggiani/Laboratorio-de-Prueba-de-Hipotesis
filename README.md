# Laboratorio Interactivo de Prueba de Hipótesis

Herramienta visual e interactiva para explorar inferencia estadística clásica sobre la media y la varianza poblacional, construida en HTML/JS puro sin dependencias de backend.

## Demo

Abrí el `demo`(./index.html) directamente en el navegador — no requiere servidor.

## ¿Qué hace?

El laboratorio:

1. **Genera una población** de N = 100.000 observaciones ~ N(μ, σ²) configurables, usando el método de Box-Muller.
2. **Extrae 10 muestras independientes** de tamaño n del mismo proceso generativo.
3. **Computa** media muestral x̄ y varianza muestral s² para cada muestra.
4. **Ejecuta dos pruebas de hipótesis** por muestra:
   - **t-test de una muestra** — H₀: μ = μ₀ — estadístico t = (x̄ − μ₀) / (s/√n) ~ t(n−1)
   - **χ²-test de varianza** — H₀: σ² = σ₀² — estadístico T = (n−1)s²/σ₀² ~ χ²(n−1) bajo H₀
5. **Visualiza** tres capas de distribución:
   - Histograma de densidad de la población con curva N(μ, σ²) teórica superpuesta.
   - Distribución muestral de x̄ ~ N(μ, σ²/n) con regiones de rechazo y las 10 medias muestrales proyectadas.
   - Distribución del estadístico T = (n−1)s²/σ₀² ~ χ²(n−1) bajo H₀ con regiones de rechazo y los 10 estadísticos proyectados.
   - Histograma individual de la muestra seleccionada (clic en cualquier fila de la tabla).

## Parámetros configurables

| Parámetro | Descripción | Default |
|-----------|-------------|---------|
| μ | Media de la distribución poblacional | 50 |
| σ | Desvío estándar poblacional | 10 |
| n | Tamaño de cada muestra | 50 |
| μ₀ | Media bajo H₀ (t-test) | 50 |
| σ₀² | Varianza bajo H₀ (χ²-test) | 100 |
| α | Nivel de significancia | 0.05 |

## Experimentos sugeridos

- **H₀ verdadera**: dejá μ₀ = μ y σ₀² = σ². La tasa de rechazo debería rondar α (error tipo I).
- **H₀ falsa en media**: cambiá μ₀ a μ + 1σ. Observá cómo los x̄ migran hacia la región de rechazo.
- **Efecto del tamaño de muestra**: aumentá n → la curva muestral se angosta y la potencia del test sube.
- **Control del nivel α**: reducí α a 0.01 → las regiones de rechazo se achican y caen menos muestras en ellas.

## Implementación estadística

Todas las funciones están implementadas en JS puro, sin librerías externas de estadística:

- **Box-Muller** — generación de variables normales.
- **Función beta incompleta regularizada** (método de fracciones continuas) — p-valor del t-test.
- **Función gamma incompleta** (series + fracciones continuas) — p-valor del χ²-test.
- **Inversas numéricas** de t y χ² por búsqueda binaria — valores críticos para regiones de rechazo.

## Dependencias externas

| Librería | Versión | Uso |
|----------|---------|-----|
| [Chart.js](https://www.chartjs.org/) | 4.4.1 | Gráficos |
| [Tabler Icons](https://tabler.io/icons) | 3.31.0 | Íconos UI |

Ambas se cargan desde CDN — no hay `package.json` ni paso de build.

## Estructura del repositorio

```
.
├── index.html   # Aplicación completa (autocontenida)
└── README.md
```

## Uso

```bash
git clone https://github.com/fcontiggiani/<repo>.git
cd <repo>
# Abrir index.html en el navegador, o:
python -m http.server 8080
```

## Nota conceptual

> s² **no** sigue una distribución χ². Lo que sigue una χ²(n−1) bajo H₀ es el estadístico de prueba T = (n−1)s²/σ₀². La relación exacta es s² ~ [σ²/(n−1)] · χ²(n−1). El gráfico muestra la distribución de T, no de s².

## Licencia

MIT
