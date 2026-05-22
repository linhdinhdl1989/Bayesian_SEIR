# Bayesian SEIR/TB Compartment Model

## Overview

This repository contains a Bayesian compartmental modeling analysis of tuberculosis incidence using Julia and Turing.jl. The analysis is implemented in `Project_TB.ipynb` and fits a time-dependent TB transmission model to historical incidence data.

## Files

- `Project_TB.ipynb` - Julia notebook containing data loading, model definition, Bayesian inference, and visualization.
- `Project_TB.html` - HTML export of the notebook for static viewing.
- `tuberculosis.csv` - historical TB incidence data with `Year` and `Case` columns.
- `README.md` - project documentation.

## Model Description

The notebook implements a TB-specific compartmental model derived from SEIR-style dynamics with the following compartments:

- `S` : susceptible population
- `L` : latent TB cases
- `Ti`: infectious treated TB cases
- `Tn`: infectious non-treated TB cases
- `R` : recovered or removed individuals
- `tTB`: cumulative TB incidence

Key model features:

- Time-varying transmission rate `β(t)` defined as:
  `β(t) = β₀ / (1 + b D_β t)^{1/b}`
- Time-varying treatment-related removal rate `μ_T(t) = μ_{T0} / (1 + D_μ t)`
- Bayesian inference with priors on epidemiological parameters such as:
  - mean infectious period `μ⁻`
  - progression and treatment proportions `p`, `f`, `q`, `ω`, `c`
  - base incidence scaling `AveI`
  - time variation factors `b`, `D_β`, `D_μ`
- Observation model using a Negative Binomial likelihood to fit reported incident TB cases.

## Data

The dataset `tuberculosis.csv` contains two columns:

- `Year` — calendar year
- `Case` — reported TB incidence for that year

The notebook reads the data in reverse chronological order, fits the model, and computes posterior summaries for transmission and reproduction metrics.

## Requirements

This project is built for Julia. The notebook uses the following packages:

- `Turing`
- `DifferentialEquations`
- `RecursiveArrayTools`
- `CSV`
- `DataFrames`
- `Plots`
- `StatsPlots`
- `LazyArrays`
- `Random`
- `LaTeXStrings`

## Usage

1. Open `Project_TB.ipynb` in a Julia-capable notebook environment such as Jupyter or Pluto.
2. Ensure the `tuberculosis.csv` file is present in the same directory.
3. Install the required Julia packages if needed, for example:

```julia
using Pkg
Pkg.add.( ["Turing", "DifferentialEquations", "RecursiveArrayTools", "CSV", "DataFrames", "Plots", "StatsPlots", "LazyArrays", "LaTeXStrings"] )
```

4. Run the notebook cells to:
   - load the dataset
   - define and solve the TB compartmental model
   - sample the posterior distribution with NUTS
   - generate posterior plots for `β(t)`, `μ_T(t)`, and `R_t`

## Outputs

The notebook produces posterior inference results and saves model diagnostic plots such as:

- `beta.png`
- `muT.png`
- `Rt.png`

## Notes

This repository represents a Bayesian application of compartmental modeling to tuberculosis incidence data, emphasizing time-varying transmission and treatment dynamics.
