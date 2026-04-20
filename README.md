[README (2).md](https://github.com/user-attachments/files/26905366/README.2.md)
# Thermal Conductivity Modeling of a Copper Bar

A GitHub-ready research notebook for modeling heat conduction in an instrumented copper bar using analytical, finite-difference, and physics-informed approaches.

## Overview

This project analyzes temperature evolution measured by 11 thermocouples mounted along a copper bar. The notebook compares several modeling approaches against experimental data:

- **Analytical Fourier-series model**
- **1D finite-difference heat equation**
- **Boundary-condition-driven models using measured thermocouple data**
- **Radial heat-loss fitting and sensitivity analysis**
- **Chi-squared, residual, and RMSE diagnostics**
- **Physics-Informed Neural Network (PINN) extension**

The repository is organized so it can be uploaded directly to GitHub and run locally once the raw Excel datasets are placed in the `data/` folder.

## Repository Structure

```text
thermal-conductivity-modeling/
├── README.md
├── .gitignore
├── requirements.txt
├── requirements-pinn.txt
├── thermal_conductivity_modeling.ipynb
├── data/
│   └── README.md
├── figures/
│   └── .gitkeep
└── outputs/
    └── .gitkeep
```

## Required Data Files

The raw experimental Excel files are **not included** in this upload bundle. Place them in the `data/` folder using these filenames:

- `run_1.xlsx`
- `run_2.xlsx`
- `run_3.xlsx`
- `Run_4.xlsx`

The notebook includes logic to detect common duplicate-upload variants such as `run_2(1).xlsx`.

## Getting Started

Create and activate a virtual environment, then install the core dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

If you want to run the PINN section as well, install the TensorFlow extras:

```bash
pip install -r requirements-pinn.txt
```

Start Jupyter:

```bash
jupyter lab
```

Then open:

```text
thermal_conductivity_modeling.ipynb
```

## Core Workflow

1. Place the Excel files in `data/`
2. Open the notebook
3. Select the desired run using `active_run`
4. Execute the notebook from top to bottom
5. Review generated figures in `figures/`
6. Review exported text / CSV outputs in `outputs/`

## Methods Summary

### Finite-Difference Modeling
The main workflow solves the 1D heat equation along the bar using an explicit finite-difference scheme with a stability check on the diffusion number.

### Boundary Conditions
Several models are compared:
- idealized constant-temperature boundaries
- measured hot-end boundary only
- measured hot- and cold-end boundaries
- measured boundaries with radial heat-loss correction

### Model Evaluation
Model quality is assessed using:
- chi-squared
- reduced chi-squared
- per-thermocouple RMSE
- residual plots
- sensitivity to thermal diffusivity and fitted radial loss

## PINN Extension

The GitHub version of this project includes a **physics-informed neural network (PINN)** section as a portfolio-facing extension beyond the core lab analysis.

The PINN section:
- trains a neural network on the thermocouple temperature data
- penalizes violations of the 1D heat equation during training
- treats thermal diffusivity as a learnable parameter
- compares learned predictions against the measured temperature field
- exports prediction, error, residual, and training-history outputs

### PINN Outputs

When the PINN cells are run, the notebook saves the following files to `outputs/`:

- `pinn_prediction_matrix.txt`
- `pinn_error_matrix.txt`
- `pinn_pde_residual_matrix.txt`
- `pinn_training_history.csv`
- `pinn_summary.txt`

It also saves PINN figures to `figures/`, including:
- training-loss curves
- measured vs predicted heatmaps
- profile comparisons at snapshot times
- error trends vs time and position
- thermocouple time-trace comparisons
- PDE residual visualization
- predicted vs measured scatter

## Notes for GitHub Presentation

- The notebook filename has been cleaned for a professional repository upload.
- Generated figures and text outputs are separated from source files.
- Raw data files are expected in `data/` rather than the repository root.
- The PINN section is preserved for portfolio presentation, while still remaining optional from a dependency standpoint.
- `.gitignore` is configured to avoid committing generated outputs and local environment files.

## Suggested Next GitHub Steps

Before uploading, consider:
- adding a license file if you want others to reuse the code
- adding a few representative figures to the repository once generated
- including a short project description in the GitHub repository “About” section
- pinning one or two PINN result images in the repository README once you generate them

## Author

Prepared for academic / research presentation and GitHub portfolio upload.
