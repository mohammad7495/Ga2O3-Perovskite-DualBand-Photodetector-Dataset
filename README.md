# Ga2O3-Perovskite-DualBand-Photodetector-Dataset
FEM-generated dataset for physics-guided surrogate modeling and optimization of self-powered Ga2O3/perovskite dual-band photodetectors.

# Dataset for Physics-Guided Surrogate Modeling and Multi-objective Optimization of Self-Powered Ga2O3/Perovskite Dual-Band Photodetectors

## Overview

This repository contains the simulation dataset generated for the study:

**“Physics-Guided Surrogate Modeling and Multi-objective Optimization of Self-Powered Ga2O3/Perovskite Dual-Band Photodetectors”**

The dataset was generated using a validated finite-element-method (FEM) framework for zero-bias Ga2O3/perovskite photodetectors. The design space includes different perovskite absorbers, hole-transport-layer (HTL) configurations, layer thicknesses, doping concentrations, electronic material properties, and band-alignment descriptors.

The final dataset contains **3,942 successfully simulated device configurations**, spanning **11 perovskite compositions** and **8 HTL states**, including seven HTL materials and the HTL-free configuration.

The dataset was used for:
- surrogate-model development,
- comparison of material-aware and descriptor-based feature representations,
- prediction of the ultraviolet and second-band responsivities,
- model interpretation using SHAP and partial-dependence analysis,
- and surrogate-assisted optimization using QPSO and NSGA-II.

## Dataset file

The main dataset is provided as:

`FEM_photodetector_dataset.xlsx`

Each row corresponds to one successfully simulated photodetector configuration, while the columns contain material identities, structural and electronic parameters, derived band-alignment descriptors, simulated photocurrents, and responsivities.

## Dataset columns

| Column | Description | Unit / Type |
|---|---|---|
| `perovskite` | Perovskite absorber material used in the simulated device | Categorical |
| `htl_name` | Hole-transport-layer material; indicates the HTL used in the device configuration | Categorical |
| `t_perovskite_nm` | Thickness of the perovskite absorber layer | nm |
| `t_Ga2O3_nm` | Thickness of the Ga2O3 layer | nm |
| `t_HTL_buffer_nm` | Thickness of the HTL/buffer layer; set to zero for HTL-free structures | nm |
| `N_A` | Acceptor concentration in the perovskite layer | cm^-3 |
| `N_D` | Donor concentration in the Ga2O3 layer | cm^-3 |
| `N_A_HTL` | Acceptor concentration in the HTL | cm^-3 |
| `chi_perov_V` | Electron affinity of the perovskite absorber | eV |
| `lam_Vis_nm` | Wavelength associated with the second spectral-response region | nm |
| `has_HTL` | Binary indicator specifying whether an HTL is present | 0/1 |
| `Eg_perov_eV` | Bandgap of the perovskite absorber | eV |
| `Eg_HTL_eV` | Bandgap of the HTL material | eV |
| `chi_HTL_eV` | Electron affinity of the HTL material | eV |
| `VBO_eV` | Valence-band offset used to describe the relevant heterointerface band alignment | eV |
| `CBO_eV` | Conduction-band offset used to describe the relevant heterointerface band alignment | eV |
| `VBO_abs_eV` | Absolute magnitude of the valence-band offset | eV |
| `CBO_abs_eV` | Absolute magnitude of the conduction-band offset | eV |
| `I_UV_A` | Simulated device current associated with the ultraviolet response | A |
| `I_Vis_A` | Simulated device current associated with the second spectral response | A |
| `R_UV` | Simulated ultraviolet responsivity | A/W |
| `R_Vis` | Simulated responsivity in the second spectral-response region | A/W |

## Feature groups

For convenience, the dataset variables can be grouped into the following categories:

### Material identity
- `perovskite`
- `htl_name`
- `has_HTL`

### Geometrical parameters
- `t_perovskite_nm`
- `t_Ga2O3_nm`
- `t_HTL_buffer_nm`

### Doping parameters
- `N_A`
- `N_D`
- `N_A_HTL`

### Electronic-material descriptors
- `chi_perov_V`
- `Eg_perov_eV`
- `Eg_HTL_eV`
- `chi_HTL_eV`

### Band-alignment descriptors
- `VBO_eV`
- `CBO_eV`
- `VBO_abs_eV`
- `CBO_abs_eV`

### Spectral/output quantities
- `lam_Vis_nm`
- `I_UV_A`
- `I_Vis_A`
- `R_UV`
- `R_Vis`

## Notes

- The simulations correspond to **zero external bias** operation.
- `has_HTL = 0` denotes an HTL-free configuration, while `has_HTL = 1` denotes a structure containing an HTL.
- For HTL-free structures, the HTL thickness is set to zero.
- `R_UV` and `R_Vis` are the two target photoresponses used for surrogate-model development.
- Although the variable name `R_Vis` is retained in the dataset for consistency with the simulation workflow, it represents the **second spectral-response channel** considered in the study.
- The dataset contains only successfully completed FEM simulations used in the subsequent machine-learning analysis.

## Related analysis

The dataset was used to train and evaluate several regression models, including multilayer perceptron (MLP), CatBoost, XGBoost, LightGBM, Extra Trees, Random Forest, SVR, KNN, and Ridge regression.

Two complementary feature representations were considered:

- **Model A (material-aware):** includes explicit perovskite and HTL identities together with numerical descriptors.
- **Model B (descriptor-based):** excludes explicit material identities and uses only numerical physical descriptors for model interpretation.

Model A was primarily used for surrogate-assisted design-space exploration, whereas Model B was used for SHAP and partial-dependence analyses.

## Data availability

The dataset is provided to support reproducibility and independent analysis of the results reported in the associated manuscript.
