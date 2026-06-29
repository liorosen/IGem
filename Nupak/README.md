# NUPACK First Steps

This folder contains the NUPACK tutorial track. It is aimed at readers who are
comfortable with basic Python and nucleic-acid vocabulary but new to NUPACK.
The track moves from a single isolated complex, to the thermodynamic
ensemble, to test-tube equilibrium among many species, and finally to
sequence design (single complex -> constrained complex -> multi-tube
orthogonal design).

## Current Notebooks

- `01_introduction.ipynb` - NUPACK basics: `Model`, `Strand`, `Complex`, and `complex_analysis` for a single complex, including the MFE structure, dot-parens-plus notation, the pair-probability matrix, and a `forgi`-based structure diagram.
- `02_structural_analysis.ipynb` - MFE vs. suboptimal structures (`compute=["subopt"]`), energy gaps, and multi-strand complexes using dot-parens-plus notation with `+`.
- `03_probabilities.ipynb` - the partition function and ensemble free energy, pair probabilities vs. the MFE structure, structure sampling (`compute=["sample"]`), and how the ensemble shifts with temperature.
- `04_defect_analysis.ipynb` - the ensemble defect (`defect(...)`): why low energy isn't the same as matching a target structure, normalized defect, and per-nucleotide defect profiles.
- `05_basic_tube_analysis.ipynb` - `Tube` and `tube_analysis`: equilibrium concentrations, yield, and competition between strands in a mixture.
- `06_adv_tube_analysis.ipynb` - condition sweeps over temperature, salt, and concentration, producing melting-curve-style figures and a `melting_temperature` helper.
- `07_intro_design.ipynb` - first steps with `Domain`, `TargetStrand`, `TargetComplex`, `TargetTube`, and `tube_design`: designing a hairpin and a duplex, then closing the loop with `complex_analysis`/`tube_analysis`.
- `08_design_constraints.ipynb` - constrained design: IUPAC domain alphabets, fixed and complementary (`~domain`) domains, and `Pattern`/`Diversity` sequence constraints.
- `09_tube_design.ipynb` - multi-complex tube design with `off_targets=SetSpec(...)`, and a crosstalk matrix that verifies a library of designed strands is orthogonal.
- `10_multitube_design.ipynb` - capstone case study: a single designed sequence with different on-target structures in different tubes (a context-dependent "switch"), verified with a full re-analysis dashboard.

## Visualization strategy

- **Structure diagrams** for single complexes and simple two-strand complexes use `forgi` (`forgi.graph.bulge_graph` + `forgi.visual.mplotlib`), the same library as the ViennaRNA track.
- **Matrices and sweeps** (pair-probability matrices, crosstalk matrices, defect/condition sweeps) use seaborn heatmaps and line plots with a shared `sns.set_theme(style="whitegrid")`.
- **Tube composition** (species concentrations across complexes/conditions) uses stacked bar charts.
- **Design quality** (ensemble defect, per-nucleotide defect) uses bar charts and per-position profile plots.

Each notebook is designed to run independently from a clean kernel.

## Environment

NUPACK is not installed from the normal PyPI index. Install it from your
NUPACK wheel or local NUPACK package first, then install the general tutorial
dependencies:

```bash
python -m venv venv
source venv/bin/activate
pip install /path/to/nupack-4.0.2.0-*.whl
pip install -r requirements.txt
```

If you already have NUPACK installed in your environment, only run the final
`pip install -r requirements.txt` line.

## Verifying the Course

To execute every notebook from a clean kernel and write executed outputs back
into the files:

```bash
for nb in *.ipynb; do
  jupyter nbconvert --to notebook --execute --inplace "$nb" --ExecutePreprocessor.timeout=900
done
```

To test execution without modifying the repository, write outputs to a
temporary directory:

```bash
mkdir -p /tmp/nupack_tutorial_execute
for nb in *.ipynb; do
  jupyter nbconvert --to notebook --execute "$nb" --output "/tmp/nupack_tutorial_execute/$nb" --ExecutePreprocessor.timeout=900
done
```

Sequence-design notebooks (7-10) are stochastic, so exact designed sequences
may differ between executions; the qualitative behavior and low defects
should remain stable.
