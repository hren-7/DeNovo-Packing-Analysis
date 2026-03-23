
# De Novo Core Packing Analysis: Geometric Limitations

## Overview
This repository contains a Python-based geometric analysis pipeline (`Bio.PDB`, `scipy.spatial`) designed to evaluate steric clashing and core overpacking in *de novo* protein designs. 

The project was inspired by the 2025 preprint *Using experimental results of protein design to guide biomolecular energy-function development* (Haddox, Rocklin, Baker, DiMaio et al.), which identified systematic biases in the Rosetta `fa_rep` energy term allowing for subtle soft-clashes in hydrophobic cores.

## Methodology & Findings
The script parses heavy-atom coordinates and calculates Euclidean distances across a recalibrated 3.2 Å threshold to capture soft-clashing (a 0.20 Å penetration into the Carbon-Carbon van der Waals radius). 

The pipeline was benchmarked against a hyperstable positive control (Top7 / 1QYS) and a known computationally failed design (`HEEH_rd4_0640` from the Rocklin 2017 dataset). 

**Conclusion:** The raw geometric analysis successfully highlighted the limitations of using static distance thresholds for stability prediction. 
1. The 3.2 Å threshold inadvertently captures stabilizing hydrogen bonds (N-O, C-O), inflating the clash ratios of stable proteins.
2. Rosetta's minimizer satisfies internal constraints even in unstable models, resulting in near-zero C-C overlaps. 

This confirms the necessity of utilizing distributional mathematics (KL divergence of atom-pair distances) over single-structure geometric proxies.

## Repository Contents
* `steric_clash_analysis_current.ipynb`: The raw, vectorized Euclidean distance pipeline.
* `StericClashAnalysis_HorryRen.pdf`: The executive summary, metric comparisons, and pair-type breakdown charts. 
* `/data`: The PDB coordinate files used for benchmarking.
