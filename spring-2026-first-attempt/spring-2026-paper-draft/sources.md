# Sources

> Part of our spring 2026 paper draft, copied as written. See the corrections in `../README.md`.

## General Sourcing

National Center for Biotechnology Information (2026). PubChem Compound Summary for CID 3386, Fluoxetine. Retrieved June 15, 2026 from https://pubchem.ncbi.nlm.nih.gov/compound/Fluoxetine.

National Center for Biotechnology Information (2026). PubChem Compound Summary for CID 60835, Duloxetine. Retrieved June 15, 2026 from https://pubchem.ncbi.nlm.nih.gov/compound/Duloxetine.

National Center for Biotechnology Information (2026). PubChem Compound Summary for CID 2801, Clomipramine. Retrieved June 15, 2026 from https://pubchem.ncbi.nlm.nih.gov/compound/Clomipramine.

National Center for Biotechnology Information (2026). PubChem Compound Summary for CID 3100, Diphenhydramine. Retrieved June 15, 2026 from https://pubchem.ncbi.nlm.nih.gov/compound/Diphenhydramine.

National Center for Biotechnology Information (2026). PubChem Compound Summary for CID 6041, Phenylephrine. Retrieved June 15, 2026 from https://pubchem.ncbi.nlm.nih.gov/compound/Phenylephrine.

National Center for Biotechnology Information (2026). PubChem Compound Summary for CID 2725, (+-)-Chlorpheniramine. Retrieved June 15, 2026 from https://pubchem.ncbi.nlm.nih.gov/compound/Chlorpheniramine.

Nazarinasab, M., Behrouzian, F., Abdi, L., Sadegh Moghaddam, A., & Sadeghi, S. (2022). Investigating the effect of magnesium supplement in patients with major depressive disorder under selective serotonin reuptake inhibitor treatment. Journal of Family Medicine & Primary Care, 11(12), 7800–7805. https://doi.org/10.4103/jfmpc.jfmpc_1164_22

Findings from National Drug Dependence Treatment Center Broadens Understanding of Obsessive-Compulsive Disorder (Brain neurochemistry in unmedicated obsessive-compulsive disorder patients and effects of 12-week escitalopram treatment: 1 ...). (2019, June 10). Mental Health Weekly Digest, 207. https://link.gale.com/apps/doc/A588230021/AONE?u=les_main&sid=bookmark-AONE&xid=2e678497

CARLSSON, A. and LINDQVIST, M. (1969), Central and peripheral monoaminergic membrane-pump blockade by some addictive analgesics and antihistamines. Journal of Pharmacy and Pharmacology, 21: 460-464. https://doi.org/10.1111/j.2042-7158.1969.tb08287.x

Shah, J. R., Mosier, P. D., Roth, B. L., Kellogg, G. E., & Westkaemper, R. B. (2009). Synthesis, structure-affinity relationships, and modeling of AMDA analogs at 5-HT2A and H1 receptors: structural factors contributing to selectivity. Bioorganic & medicinal chemistry, 17(18), 6496–6504. https://doi.org/10.1016/j.bmc.2009.08.016

Wong, D. T., Bymaster, F. P., & Engleman, E. A. (1995). Prozac (fluoxetine, Lilly 110140), the first selective serotonin uptake inhibitor and an antidepressant drug: twenty years since its first publication. Life sciences, 57(5), 411–441. https://doi.org/10.1016/0024-3205(95)00209-o

Bloch, M. H., McGuire, J., Landeros-Weisenberger, A., Leckman, J. F., & Pittenger, C. (2010). Meta-analysis of the dose-response relationship of SSRI in obsessive-compulsive disorder. Molecular psychiatry, 15(8), 850–855. https://doi.org/10.1038/mp.2009.50

Pajouhesh, H., & Lenz, G. R. (2005). Medicinal chemical properties of successful central nervous system drugs. NeuroRx : the journal of the American Society for Experimental NeuroTherapeutics, 2(4), 541–553. https://doi.org/10.1602/neurorx.2.4.541

## Computational Sourcing

**COPILOT WAS USED TO HELP GENERATE CITATIONS**

### Software and Frameworks

- Google Colab + Python 3.11 — used for descriptor calculations, data analysis, and visualization.
  - Libraries: RDKit, pandas, numpy, matplotlib, seaborn, scipy.
  - Tasks: TPSA and LogP calculation, correlation heatmaps, linear regression, BBB prediction function, and PubChem validation.
- AutoDock Vina 1.2.7 — initial docking attempts in Colab failed due to VM execution limits; later successfully executed locally on Ellie’s Mac (M2 Pro) to generate .pdbqt complexes.
- ORCA 5.0.3 (MacOS Intel build under Rosetta 2) — used for all DFT calculations and Mg²⁺ complexation.
  - Functional: B3LYP | Basis set: def2‑SVP | SCF settings: MaxIter 300, SOSCF, Damp 0.30, Shift 0.30.
  - Tasks: single‑point energy calculations and electronic structure analysis for Mg‑ligand complexes.
- Microsoft Copilot — Accessed via Microsoft Edge and Google Colab integration. © Microsoft Corporation, 2026.
  - Assisted in structuring Python workflows and debugging RDKit descriptor calculations
  - Generated these citations
- ChimeraX 1.7 — molecular visualization and Mg²⁺ complex inspection.
  - Used to measure Mg–O/N distances, color‑code atoms, and create publication‑ready images.
- Zotero — reference management for literature and database citations.

### Databases and Sources

- PubChem Database (National Center for Biotechnology Information, NIH) — used for SMILES strings, compound CIDs, and empirical TPSA/LogP validation.
  - Example CIDs: Fluoxetine 3386, Duloxetine 60877, Clomipramine 2801, Salicylic Acid 338, Naproxen 156391, Chlorpheniramine 2725.
  - URL: https://pubchem.ncbi.nlm.nih.gov

### Descriptors and Analytical Criteria

- Topographic Polar Surface Area (TPSA) ≤ 90 Å² → optimal CNS penetration.
- Lipophilicity (LogP) between 2.0 and 5.0 → balanced membrane permeability.
- BBB Prediction Logic: Molecules meeting both thresholds → likely permeable; confidence score based on distance from threshold.
- Regression and Correlation Analysis: Linear regression between TPSA and LogP to quantify polarity vs lipophilicity; seaborn.heatmap(df.corr(), annot=True) for descriptor interrelationships; scatter plots with regression line, R², and color‑coded BBB prediction.

### References for Computational Methods

- Neese, F. The ORCA Quantum Chemistry Program Package 5.0.3. Max Planck Institute for Chemical Energy Conversion.
- Pettersen et al. UCSF ChimeraX: Structure Visualization for Researchers, Educators, and Developers. Protein Science (2021).
- Trott & Olson. AutoDock Vina: Improving the Speed and Accuracy of Docking. J. Comput. Chem. (2010).
- Landrum, G. RDKit: Open‑Source Cheminformatics.
- Kim et al. PubChem Database. Nucleic Acids Research (2023).
- Waskom, M. et al. Seaborn: Statistical Data Visualization. Journal of Open Source Software (2021).
- Virtanen, P. et al. SciPy 1.0: Fundamental Algorithms for Scientific Computing in Python. Nature Methods (2020).
- Pedregosa, F. et al. Scikit‑learn: Machine Learning in Python. JMLR (2011).
- Hunter, J. D. Matplotlib: A 2D Graphics Environment. Computing in Science & Engineering (2007).
- Van Rossum, G. & Drake, F. L. Python 3 Reference Manual. (2009).
