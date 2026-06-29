# ViennaRNA Tutorial Curriculum Plan

This is a proposed first-step tutorial track for ViennaRNA. It is intentionally a plan only; notebooks should be created after the lesson order and scope are approved.

## Intended Audience

Readers who are comfortable with basic Python and RNA secondary-structure vocabulary, but are new to ViennaRNA. The track should complement the NUPACK notebooks by emphasizing ViennaRNA's command-line tools and Python bindings for single-sequence folding, ensemble analysis, and comparative workflows.

## Proposed Lesson Sequence

| Lesson | Proposed filename | Main topics | Goal |
| :--- | :--- | :--- | :--- |
| **1. Introduction to ViennaRNA** | `01_introduction.ipynb` | Package overview, RNAfold CLI, Python `RNA` module, dot-bracket notation | Run the simplest fold from both CLI-style and Python APIs. |
| **2. Minimum Free-Energy Folding** | `02_mfe_folding.ipynb` | `RNA.fold`, fold compounds, MFE structure, free energy interpretation | Understand the core MFE workflow and its assumptions. |
| **3. Partition Function and Base-Pair Probabilities** | `03_partition_probabilities.ipynb` | `pf()`, ensemble free energy, base-pair probability matrix, dot plots | Move from one structure to ensemble probabilities. |
| **4. Suboptimal Structures and Structural Diversity** | `04_suboptimal_structures.ipynb` | Suboptimal folds, energy windows, stochastic backtracking | Explore alternative folds and structural uncertainty. |
| **5. Constraints and Forced Pairing** | `05_constraints.ipynb` | Hard constraints, soft constraints, forced/unpaired positions | Learn how to guide folding with known structural information. |
| **6. Consensus and Comparative Folding** | `06_comparative_folding.ipynb` | RNAalifold concepts, alignments, covariation, consensus structures | Use related sequences to improve structure prediction. |
| **7. RNA-RNA Interaction Basics** | `07_interactions.ipynb` | RNAcofold concepts, duplex/intermolecular structures, interaction energy | Analyze simple interactions between two RNA strands. |
| **8. Temperature and Parameter Effects** | `08_environment_effects.ipynb` | Temperature changes, model details, parameter choices | Show how physical/model choices affect predicted structures. |
| **9. Visualization Workflows** | `09_visualization.ipynb` | ViennaRNA SVG drawings, dot plots, arc diagrams, pairing matrices, explanatory charts | Build clear visual interpretations of ViennaRNA outputs. |
| **10. Practical Case Study** | `10_case_study.ipynb` | End-to-end analysis of a small RNA or designed toy system | Combine MFE, ensemble, constraints, and visualization in one workflow. |

## Suggested Teaching Style

- Keep examples small and fast enough to execute from a clean kernel.
- Use both ViennaRNA command-line concepts and Python bindings, but implement notebooks in Python.
- Prefer native ViennaRNA visualization outputs, especially SVG structure drawings and dot plots, supplemented by Matplotlib charts where they clarify interpretation.
- Make contrasts with NUPACK explicit only when helpful; avoid turning the track into a tool comparison.
- Add interpretation after every plot or table.

## Open Decisions Before Notebook Creation

- Whether to require the ViennaRNA Python package only, or also demonstrate shell commands such as `RNAfold`.
- Whether comparative folding should use a tiny toy alignment or a real curated alignment.
- Whether the final case study should focus on riboswitch-like folding, antisense interaction, or general structure prediction.
- Which native ViennaRNA visual outputs should be emphasized in each lesson versus saved for the dedicated visualization lesson.
