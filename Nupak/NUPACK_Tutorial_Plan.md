# NUPACK Tutorial Curriculum Plan

This is a 10-lesson course for readers who are comfortable with basic Python and
nucleic-acid vocabulary but new to NUPACK. The track moves from a single isolated
complex, to the thermodynamic ensemble, to test-tube equilibrium among many species,
and finally to sequence design (single complex -> constrained complex -> multi-tube
orthogonal design). Each notebook runs independently from a clean kernel and ends
with a short "what's next" pointer plus 1-2 exercises.

## Visualization strategy

- **Structure diagrams** (single complex, pseudoknot-free): use **forgi** (same
  library as the ViennaRNA track) on the per-strand dot-bracket portion of NUPACK's
  dot-parens-plus output. This keeps structure pictures consistent across both
  tracks and ties each diagram to the nearest-neighbor element types (stem, hairpin,
  interior loop, multiloop, dangling end).
- **Matrices and sweeps** (pair-probability matrices, crosstalk matrices, defect vs.
  parameter sweeps): seaborn heatmaps/line plots with a shared theme
  (`sns.set_theme(style="whitegrid")`), set once in lesson 1 and reused throughout.
- **Tube composition** (species concentrations across complexes/conditions): stacked
  bar charts / area plots - a chart type not used elsewhere in the series, chosen
  because it directly answers "what is actually in the tube?".
- **Design quality** (ensemble defect, per-nucleotide defect): bar/lollipop charts
  and per-position profile plots, reusing the profile-plot idiom from the
  ViennaRNA track (`09_visualization.ipynb`) so readers see the same chart shape
  applied to a new quantity.
- RNAvigate is **dropped** from this track. Its circular/secondary-structure objects
  expect a single linear RNA with real 2D coordinates; bending NUPACK's
  multi-strand, defect- and concentration-centric outputs into that shape required
  synthetic coordinates and added more glue code than insight. forgi covers the
  structure-diagram need for single complexes, and the analytical plots above cover
  everything multi-strand/tube/design related.

## Lesson Sequence

| Lesson | Filename | Prerequisites | Main topics | Key API | Goal |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1. NUPACK Basics** | `01_introduction.ipynb` | None | `Model`, `Strand`, `Complex`, `complex_analysis`, MFE, dot-parens-plus, pair probability matrix | `Model`, `Strand`, `Complex`, `complex_analysis(compute=["pfunc","mfe","pairs"])` | Learn the core objects and run one complete single-complex analysis, with a forgi structure diagram. |
| **2. Structural Analysis** | `02_structural_analysis.ipynb` | 1 | MFE vs. suboptimal structures, energy gaps, multi-strand complexes, dot-parens-plus with `+`, strand permutations | `compute=["subopt"]`, multi-`Strand` `Complex`, `result.subopt` | Understand structural alternatives and how NUPACK represents multi-strand complexes. |
| **3. Thermodynamic Probabilities** | `03_probabilities.ipynb` | 1, 2 | Partition function, ensemble free energy, pair probabilities vs. MFE, structure sampling, temperature dependence | `compute=["sample"]`, `result.free_energy`, `result.pairs` | Move from single structures to ensemble-level interpretation; see how the ensemble shifts with temperature. |
| **4. Ensemble Defect** | `04_defect_analysis.ipynb` | 3 | Target-structure energy vs. MFE energy, ensemble defect, normalized defect, per-nucleotide defect profile | `compute=["pfunc","mfe","pairs"]`, `defect(...)` | Learn why low energy is not the same as matching a desired structure - the quantity later used as the design objective. |
| **5. Basic Tube Analysis** | `05_basic_tube_analysis.ipynb` | 1-4 | `Tube`, initial strand concentrations, `tube_analysis`, equilibrium complex concentrations, yield, competition | `Tube`, `tube_analysis(tubes=[...], compute=["pfunc","mfe","pairs","sample"])` | Predict what species actually form in a mixture of strands, not just one complex in isolation. |
| **6. Advanced Tube Analysis** | `06_adv_tube_analysis.ipynb` | 5 | Condition sweeps: temperature (melting curves), salt, strand concentration, GC content | repeated `Model`/`Tube`/`tube_analysis` over a parameter grid | Explore how physical conditions shift tube equilibrium, building melting-curve-style figures. |
| **7. Introduction to Design** | `07_intro_design.ipynb` | 1-6 | `Domain`, `TargetStrand`, `TargetComplex`, `TargetTube`, `tube_design`, hairpin and duplex design, defect reports | `Domain`, `TargetStrand`, `TargetComplex`, `tube_design(tubes=[...])`, `design.report()` | Design simple sequences for a target structure and verify them by re-running the analysis from lessons 1-4. |
| **8. Design with Constraints** | `08_design_constraints.ipynb` | 7 | IUPAC domain alphabets, fixed/complementary domains, sequence `Pattern` constraints, `Diversity` constraints | `Domain(... , dna/rna alphabets)`, `Pattern`, `Diversity` | Guide design toward sequences that also satisfy synthesis/biological constraints (no long repeats, fixed motifs). |
| **9. Tube Design and Orthogonality** | `09_tube_design.ipynb` | 7, 8 | Multi-complex tube design, off-target complex suppression, crosstalk matrix between designed strands | multiple `TargetComplex`/`TargetTube` with off-target complexes, pairwise `complex_analysis` for crosstalk | Design several intended complexes that coexist in one tube with low pairwise crosstalk. |
| **10. Multi-Tube Design Case Study** | `10_multitube_design.ipynb` | 1-9 | End-to-end case study: multi-environment design, ON/OFF target tubes, post-design verification dashboard | multiple `TargetTube`s with different `on_targets`/`off_targets`, full re-analysis of the final sequence set | Design one set of sequences with different intended behavior in different tubes (e.g. ON in one tube, OFF in another), then verify with the analysis tools from earlier lessons. |

## Maintenance Notes

- Lessons 1-4 stay scoped to a *single* complex/ensemble; tube-level reasoning is
  introduced starting in lesson 5. Don't pull `Tube`/`tube_analysis` forward into
  lessons 1-4 even as a teaser.
- After lesson 3 establishes the partition function and pair probabilities, later
  lessons should reference those concepts rather than re-deriving them.
- Keep forgi structure diagrams to single-strand or simple two-strand complexes
  where the dot-bracket portion is unambiguous; for larger multi-strand complexes in
  lessons 2, 9, 10, prefer the analytical plots (concentration/defect/crosstalk)
  over forcing a structure diagram.
- Each design lesson (7-10) should close the loop by re-analyzing the designed
  sequence with `complex_analysis`/`tube_analysis` from earlier lessons, so design
  is never presented as a black box.
