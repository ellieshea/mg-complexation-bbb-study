# Spring 2026: first attempt

My first version of the computational side (May–June 2026). Kept for the record. Final results are in `fall-2026/`.

## Files

- `spring-2026-draft.md`: our spring paper draft, copied as written
- `rdkit_analysis_colab.py`: the Colab code (SMILES → 3D, TPSA/LogP, plots, tables)
- `orca/singlepoint_template.inp`: the ORCA input template

## Corrections (found in fall 2026)

- The ORCA runs were single-point energy calculations, not docking.
- The command shown is ORCA 5.0.4, despite the "5.0.3" heading.
- The RDKit step dropped the Mg, so the "complexed" values and the conclusions drawn from them describe the free drug, not the Mg complex.
- The Computational Sourcing section lists AutoDock Vina as successful, def2‑SVP as the basis set, and ChimeraX as used. None of these is accurate: Vina never worked, the basis set was 6-31G(d), and ChimeraX wasn't used. Those citations were also generated with Copilot and have not been checked.
