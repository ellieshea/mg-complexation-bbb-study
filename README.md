# Mg²⁺ binding to OCD medications: a computational study

Ellie Shea · computational side of a joint project with Sen Partan (wet lab)

**Final results are in `fall-2026/`.** `spring-2026-first-attempt/` is my first version, kept for the record. It used single-point calculations and had a bug that dropped Mg (see Known issues).

## Research question

To what extent does magnesium‑induced complexation modify the geometry and electronic properties of SSRIs, SNRIs, and TCAs, and how do these computationally and spectroscopically observed changes affect their predicted ability to permeate the blood–brain barrier?

## Molecules

- SSRI: Fluoxetine (OTC analog: Diphenhydramine)
- SNRI: Duloxetine (OTC analog: Phenylephrine)
- TCA: Clomipramine (OTC analog: Chlorpheniramine)

## Folders

- `spring-2026-first-attempt/`: first pass (May–June 2026), all 6 molecules
  - `rdkit_analysis_colab.py`: Colab export (SMILES → 3D, TPSA/LogP, ORCA loader, 4 plots, tables) (notebook STEPS 4 + 8)
  - `orca/`: ORCA 5 single-point input template (B3LYP/6-31G(d)) (STEP 6)
- `fall-2026/`: revised pipeline (Sept–Nov 2026), the 3 real drugs
  - `01_structures/`: 3D structures + Mg placement (STEP 14)
  - `02_xtb/`: GFN2-xTB screening (STEP 15)
  - `03_dft_opt/`: ORCA 6.1.1 DFT geometry optimizations (STEP 16)
  - `04_analysis/`: charges, Mg–donor distances (STEP 17)
  - `05_bsse/`: counterpoise (BSSE) correction (STEP 18)
  - `06_rdkit/`: RDKit round 2, Mg bonded (STEP 21)
  - `07_water/`: explicit first-shell water complexes (STEPS 24–25)

The full story (decisions, problems, readings) is in my research notebook.

## Tools

- Python 3, RDKit, pandas, NumPy, SciPy, matplotlib, seaborn, scikit-learn
- ORCA 5.0.4 (spring), ORCA 6.1.1 (fall)
- xtb (GFN2-xTB)

## Known issues in the spring code

- The ORCA → RDKit loader skips any atom not in `ORGANIC_ELEMENTS`, so Mg was dropped from every complex. That is why ΔTPSA came out as 0.00 for most molecules in the spring results. Fixed in the fall RDKit analysis.
- `rdkit_analysis_colab.py` is the Colab export exactly as it was. `load_orca_minimal` and `remove_stray_hydrogens` are called but not defined in this export, so the file doesn't run top to bottom as-is.
- The first ORCA runs were single points, not geometry optimizations. AutoDock Vina docking was tried and abandoned (the header comment still mentions it).
