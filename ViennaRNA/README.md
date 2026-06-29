# ViennaRNA First Steps

This folder contains the ViennaRNA tutorial track.

## Current Notebooks

- `01_introduction.ipynb` - introduction to ViennaRNA: the MFE problem and nearest-neighbor energy model, dot-bracket notation, basic MFE folding with the Python `RNA` module and fold compounds, CLI-style `RNAfold` usage, native ViennaRNA SVG drawings, `forgi`-based element-type structure diagrams, seaborn-styled explanatory charts (arc diagrams, mountain plots, heatmaps, scatter/lollipop charts), best practices/pitfalls, and end-of-notebook exercises.
- `02_mfe_folding.ipynb` - the minimum free-energy workflow in depth: `RNA.fold` vs. fold compounds, reading and interpreting MFE energies, how the nearest-neighbor model assigns energy to loops and stacks, and worked examples comparing several short sequences.
- `03_partition_probabilities.ipynb` - the partition function and the Boltzmann ensemble: `fc.pf()`, base-pair probability matrices (`fc.bpp()`), positional entropy, dot plots (probabilities vs. MFE pairs), and centroid/MEA structures as ensemble-aware alternatives to the single MFE structure.
- `04_suboptimal_structures.ipynb` - exploring structural diversity below the MFE: exhaustive suboptimal enumeration with `fc.subopt(delta)`, energy windows, and stochastic ensemble sampling, with visualizations comparing competing low-energy structures.
- `05_constraints.ipynb` - guiding folding with prior knowledge: hard constraints (`hc_add_up`, `hc_add_bp`, `hc_add_from_db`) that restrict the structure space, soft constraints (`sc_add_bp`) that add pseudo-energy bonuses, and worked examples showing how constraints can recover alternative low-energy structures.
- `06_comparative_folding.ipynb` - consensus structure prediction from sequence alignments: `RNA.alifold`, consensus sequences and dot-bracket structures, mean pairwise identity, per-column conservation (positional entropy), and covariation (pscore) heatmaps that reveal compensatory mutations supporting a consensus structure.
- `07_interactions.ipynb` - RNA-RNA interactions: cofold-style two-strand fold compounds (`"seq1&seq2"`), `RNA.duplexfold`/`duplex_subopt` for RNAduplex-style intermolecular pairing, interaction free energy (ΔΔG), and base-pair probability heatmaps for a bound complex.
- `08_environment_effects.ipynb` - how temperature, salt concentration, and the energy-parameter set affect predicted structures: melting curves via repeated `RNA.md()`/`pf()` sweeps, salt-dependent stability via `md.salt`, comparing Turner2004/Turner1999/Andronescu2007 parameter sets, and a same-sequence RNA-vs-DNA thermodynamics comparison.
- `09_visualization.ipynb` - a visualization toolkit built around ViennaRNA's own 2D layout (`RNA.get_xy_coordinates`): custom structure diagrams colored by continuous quantities like base-pairing probability, comparative arc diagrams overlaying two structures on one sequence, and a multi-panel "dashboard" figure combining several chart types for one sequence.
- `10_case_study.ipynb` - an end-to-end case study tying the whole series together: a designed two-state "thermal switch" sequence analyzed via MFE, suboptimal enumeration, ensemble base-pair probabilities, a temperature sweep that locates the switch temperature, a hard constraint that overrides the temperature-driven preference, and a final before/after visualization dashboard.

## Setup

From the repository root, install the dependencies into your active Python environment:

```bash
python -m pip install -r first_steps/viennaRNA/requirements.txt
```

Then open the notebooks with Jupyter:

```bash
jupyter lab first_steps/viennaRNA
```

The tutorial plan for the full track is in `ViennaRNA_Tutorial_Plan.md`.
