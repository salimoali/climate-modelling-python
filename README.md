# climate-modelling-python

Python-based climate analysis covering temperature trends and dynamic carbon cycle modelling.

---

## 1. Canada Climate Analysis

**Notebook:** `canada_climate_analysis.ipynb`
**Data:** `canada-TAVG-monthly.txt` (Berkeley Earth), `co2_annmean_gl.txt` (NOAA GML)

### What it does

- Loads and processes Berkeley Earth fixed-width temperature anomaly data for Canada (1960–2024)
- Converts monthly anomalies to annual absolute temperatures using a -4.86°C baseline (1951–1980 reference period)
- Applies three trend methods: 11-year centred running mean, decadal averages, and linear regression
- Projects Canada's average temperature to 2050 (linear regression R² = 0.89)
- Analyses radiative forcing across albedo values 0.20–0.40 using the Stefan-Boltzmann equation
- Merges temperature data with NOAA global CO₂ concentrations and plots the relationship

### Key results

| Metric | Value |
|--------|-------|
| Warming since 1960 | ~2.8°C |
| Projected temperature 2050 (linear) | ~24.6°C |
| Radiative forcing range (1960–2024) | 3.2–3.8 W/m² |
| Regression R² | 0.89 |

---

## 2. Dynamic Carbon Cycle Model

**Notebook:** `carbon_cycle_model.ipynb`

### What it does

- Implements piecewise-linear emission functions for land-use change (from 1750) and fossil fuels (from 1850)
- Builds a six-pool carbon model: Atmosphere, Biosphere, Soils, Surface Ocean, Deep Ocean, Geosphere
- Solves the ODE system using `scipy.integrate.odeint` (Runge-Kutta)
- Runs three emission scenarios to 2100:
  - **Business-as-Usual:** ~700+ ppm CO₂
  - **Moderate Mitigation (50% cut by 2050):** ~560 ppm
  - **Aggressive Mitigation (80% cut by 2050):** ~480 ppm
- Sensitivity analysis: ocean uptake rate ±15%, land photosynthesis ±10%

### Model parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| β | 0.4 | CO₂ fertilisation factor |
| f₀ | 62 PgC yr⁻¹ | Pre-industrial biospheric uptake |
| k_ψ | 0.07 yr⁻¹ | Ocean outgassing rate constant |

### Key results

- Ocean absorbs ~30% of cumulative emissions; land sink weakens over time
- Returning to 300 ppm by 2100 requires net-negative emissions
- Ocean uptake rate is the dominant model uncertainty (±15% on projected CO₂)

---

## Requirements
numpy
pandas
matplotlib
scipy
sklearn
jupyter
pip install numpy pandas matplotlib scipy scikit-learn jupyter
---

## Data sources

- **Berkeley Earth** temperature data: https://berkeleyearth.org/high-resolution-data-access-page/
- **NOAA GML** CO₂ concentrations: https://gml.noaa.gov/ccgg/trends/gl_data.html

---

## How to run

1. Place `canada-TAVG-monthly.txt` and `co2_annmean_gl.txt` in the same directory as the notebooks
2. `jupyter notebook`
3. Run `canada_climate_analysis.ipynb` then `carbon_cycle_model.ipynb`
