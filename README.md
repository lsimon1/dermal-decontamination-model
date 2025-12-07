# Dimensionless Framework for Dermal Decontamination Modeling

Python implementation of the analytical framework for modeling dermal absorption, evaporation, and reactive neutralization of volatile chemical warfare agents and industrial toxicants.

## Overview

This repository contains Jupyter notebooks reproducing all figures from:

> Simon, L. (2025). "A dimensionless framework for modeling dermal decontamination of volatile chemical warfare agents." *Chemical Research in Toxicology* [citation details].

The framework uses two dimensionless parameters:
- **Damköhler number (Da)**: ratio of diffusion time to reaction time
- **Surface loss number (π_surf)**: combined evaporation and interfacial reaction

Three kinetic regimes are identified:
- **Low Da (< 3)**: Transport-limited (surface processes dominate)
- **Intermediate Da (3-6)**: Mixed regime (both processes important)
- **High Da (> 6-8)**: Reaction-limited (bulk neutralization dominates)

## Installation
```bash
# Clone repository
git clone https://github.com/lsimon1/dermal-decontamination-model.git
cd dermal-decontamination-model

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

## Usage

### Generating Figures

- **Fig2to7git.ipynb**: Generates Figures 2-7 from manuscript (steady-state mass fractions and effective time constants vs. Da and π_surf)
- **Fig8git.ipynb**: Generates Figure 8 (transient profiles with/without decontamination)

### Modifying for Your Scenarios

The core functions can be adapted for different agents:
```python
# Example: Compute outcomes for your agent
Da = k * h**2 / D_SC  # Your agent's Damköhler number
pi_surf = # Your surface loss number

M_abs_inf, M_surf_inf, M_reac_inf = compute_steady_state_fractions(Da, pi_surf, beta=0.2)
tau_abs, tau_surf, tau_reac = compute_effective_time_constants(Da, pi_surf, beta=0.2)

# Classify regime
if Da < 3:
    print("Transport-limited: Surface interventions critical")
elif Da < 6:
    print("Mixed regime: Both mechanisms important")
else:
    print("Reaction-limited: Chemical reactivity dominates")
```

## Key Functions

- `compute_steady_state_fractions(Da, pi_surf, beta)`: Returns absorbed, surface, and reacted mass fractions at steady state
- `compute_effective_time_constants(Da, pi_surf, beta)`: Returns characteristic timescales (98% completion) for absorption, surface loss, and reaction
- `compute_eigenvalues(Da, pi_surf)`: Solves transcendental eigenvalue equation

## Example Application: VX with RSDL

Using experimentally validated parameters:
- D_SC = 4.3×10⁻¹⁰ cm²/s
- k = 2.1×10⁻⁴ s⁻¹
- h = 13.4 μm

→ **Da ≈ 0.88** (transport-limited regime)

Model predicts 94.6% absorption reduction with 5-minute RSDL application, declining to 53% at 120 minutes—consistent with experimental data.

## Citation

If you use this code, please cite:
```
@article{simon2025decontamination,
  author = {Simon, Laurent},
  title = {A dimensionless framework for modeling dermal decontamination of volatile chemical warfare agents},
  journal = {Chemical Research in Toxicology},
  year = {2025},
  doi = {[DOI will be added upon publication]}
}
```

## License

MIT License

## Contact

Laurent Simon

## Acknowledgments
