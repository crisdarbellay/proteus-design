<div align="center">

# Proteus Design

**Backbone-explicit, thermodynamically grounded computational design of conformationally switchable proteins**

[![discovery](https://img.shields.io/badge/module-discovery-4a90d9?style=flat-square)](https://github.com/crisdarbellay/phosphoswitch-discovery)
[![evolution](https://img.shields.io/badge/module-evolution-27ae60?style=flat-square)](https://github.com/crisdarbellay/phosphoswitch-evolution)
[![design](https://img.shields.io/badge/module-design-8e44ad?style=flat-square)](https://github.com/crisdarbellay/phosphoswitch-design)
[![MD](https://img.shields.io/badge/module-MD_validation-e67e22?style=flat-square)](https://github.com/crisdarbellay/phosphoswitch-md)
[![license](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)](LICENSE)
[![paper](https://img.shields.io/badge/paper-in_preparation-red?style=flat-square)]()

</div>

---

> *Named after Proteus — the Greek sea god who could change his shape at will.
> Like the proteins it designs, the framework is built around programmable conformational change.*

---

## The story

This project started in my **first year of bachelor studies at EPFL** as a curiosity question:
*can a protein act like a molecular switch — flipping between two distinct structures depending on whether one amino acid is phosphorylated?*

What began as a literature review and a few AlphaFold2 scans grew over two years into a full computational pipeline, wet-lab expression campaign, circular dichroism experiments, mass spectrometry, and now a manuscript in preparation. The project is conducted at the **[Laboratory of Physics of Biological Systems (LPBS)](https://www.epfl.ch/labs/lpbs/)**, EPFL, under the supervision of **Prof. Sahand Jamal Rahi**.

The core finding: yes — you can not only *discover* natural phosphoswitches at proteome scale, you can also *engineer* new sequences where the switching direction and magnitude are computationally specified, and validate them experimentally.

---

## What is a phosphoswitch?

A phosphoswitch is a protein region that changes three-dimensional structure — and therefore function — when a tyrosine (or serine/threonine) is phosphorylated by a kinase. This is a form of **post-translational molecular logic**: the protein is a bistable system toggled by a chemical signal.

**Primary target: LMNA Y45** (Src kinase). A 59-aa construct centred on Y45 switches between a straight α-helix and a pulled hairpin — a **22–34 Å Cα RMSD difference** confirmed computationally and experimentally:

| Validation | Status |
|---|---|
| AlphaFold3 predictions (PTR) + Boltz 2.2 | ✓ done |
| 600 ns all-atom GROMACS simulations | ✓ done |
| Circular dichroism ±Src kinase (3 bio. reps) | ✓ done |
| FTMS top-down MS — 100% occupancy at Y45 | ✓ done |
| NMR HSQC (two-state switching at residue resolution) | planned |

Secondary validated target: **MAPRE1 Y247** (Src kinase) — expressed, CD-confirmed.

---

## Framework modules

### [phosphoswitch-discovery](https://github.com/crisdarbellay/phosphoswitch-discovery) — proteome-wide scan

Scores 15,769 kinase-substrate pairs (PhosphoSitePlus × AF2) with `switch_score_v1`. Identifies 334 high-confidence phosphoswitch candidates. Includes kinase enrichment analysis.

### [phosphoswitch-evolution](https://github.com/crisdarbellay/phosphoswitch-evolution) — directed evolution

Iterative single-mutant scan (5 rounds, ColabFold scoring). Best LMNA hit: **L20P_D25R_L37E_A42P_T49P** (RMSD 17.3 Å, score 18.6). Covers LMNA Y45 and MAPRE1 Y247.

### [phosphoswitch-design](https://github.com/crisdarbellay/phosphoswitch-design) — multi-state design

LigandMPNN on paired backbone states → 4-state PyRosetta ddG cycle → ColabFold/Boltz/AF3 validation → 11-signal consensus filter. Two designed directions: **H1** (phospho stabilises helix) and **H2** (phospho stabilises hairpin). Top hit: **22.4 Å Boltz RMSD**, 388 STRONG_SWITCH candidates from >5,500 scored.

### [phosphoswitch-md](https://github.com/crisdarbellay/phosphoswitch-md) — physics-based validation

600 ns unbiased all-atom GROMACS simulations (CHARMM36m + PTR parameters). Quantifies basin occupancy, Cα RMSD vs dual references, and phospho-driven conformational enrichment for LMNA and MAPRE1.

---

## Software stack

| Tool | Version | Role |
|------|---------|------|
| LigandMPNN | v_32_010_25 | Multi-state inverse folding (PTR-aware) |
| ColabFold | 1.5.5 | MSA-enhanced AF2 structure prediction |
| Boltz | 2.2.1 | Multimer structure prediction |
| AlphaFold3 | 3.0.3.dev | PTR-aware single-chain prediction |
| PyRosetta | 2024.26 | 4-state ddG thermodynamic cycle |
| GROMACS | 2023 | All-atom MD simulations |
| CHARMM36m | — | Force field + PTR parameters |

---

## Publication

> **Darbellay C.** *et al.* Computational discovery and design of bidirectional phosphoswitches.
> *Manuscript in preparation*, 2026.
> Laboratory of Physics of Biological Systems (LPBS), EPFL · PI: Prof. Sahand Jamal Rahi

---

## Author

**Cris Darbellay** — BSc student → researcher, EPFL
Laboratory of Physics of Biological Systems (LPBS)
[cris.darby1@gmail.com](mailto:cris.darby1@gmail.com) · [GitHub @crisdarbellay](https://github.com/crisdarbellay)

---

<div align="center">
<sub><em>"He who would learn the truth must wrestle the shape-changer."</em></sub>
</div>
