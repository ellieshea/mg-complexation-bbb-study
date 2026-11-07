# Computational Methods

> Part of our spring 2026 paper draft, copied as written. See the corrections in `../README.md`.

## Computational Modeling Application

Computational modeling can be used to predict the effects of magnesium complexation on drug geometry and blood-brain barrier (BBB) permeability, allowing for analysis of molecular properties that cannot be directly observed in a high school lab. The goal of this computational pipeline is to examine how magnesium-induced complexation modifies molecular structure and electronic properties.

### Parameters Addressed

Topological polar surface area (TPSA) measures the surface area of polar atoms within a molecule (mainly the oxygen and nitrogen atoms, along with attached hydrogens). These atoms form hydrogen bonds with water, so a high TPSA indicates that the molecule experiences strong interactions with aqueous environments. The BBB is made up of lipid membranes, through which molecules must diffuse to reach the brain. A high TPSA can be associated with stronger hydrogen bonding with water and a weaker ability to diffuse through lipid membranes, making the molecule less likely to cross the BBB.

Lipophilicity (LogP) measures how a molecule distributes between water and fat (lipid). A high LogP value indicates that the molecule is more lipophilic; it prefers fat, dissolves easily in membranes, and can cross lipid barriers such as the BBB. On the contrary, a low LogP value indicates that the molecule is less lipophilic (more hydrophilic), preferring water and with low BBB permeability.

### SMILES

According to PubChem, a trusted online chemistry database, the SMILES (Simplified Molecular Input Line Entry System) for the drugs and corresponding analogs used in the wet lab are as follows:

```
Fluoxetine: CNCCC(C1=CC=CC=C1)OC2=CC=C(C=C2)C(F)(F)F
Duloxetine: CNCC[C@@H](C1=CC=CS1)OC2=CC=CC3=CC=CC=C32
Clomipramine: CN(C)CCCN1C2=CC=CC=C2CCC3=C1C=C(C=C3)Cl
Diphenhydramine: CN(C)CCOC(C1=CC=CC=C1)C2=CC=CC=C2
Phenylephrine: CNC[C@@H](C1=CC(=CC=C1)O)O
Chlorpheniramine: CN(C)CCC(C1=CC=C(C=C1)Cl)C2=CC=CC=N2
```

SMILES represent molecules as text strings; however, most computational chemistry programs require 3D atomic coordinates to perform geometric optimization, energy calculations, or docking simulations.

### Converting to 3D Geometry

The XYZ format provides those coordinates and can list each atom’s element and its position in three‑dimensional space. To convert the SMILES into their 3D counterparts, the following code had to be assembled and run separately with each molecule's SMILES input:

```python
from rdkit import Chem
from rdkit.Chem import AllChem

# SMILES string
smiles = "CNCCC(C1=CC=CC=C1)OC2=CC=C(C=C2)C(F)(F)F"

# create molecule and add hydrogens
mol = Chem.MolFromSmiles(smiles)
mol = Chem.AddHs(mol)

# generate 3D coordinates and optimize geometry
AllChem.EmbedMolecule(mol, AllChem.ETKDG())
AllChem.UFFOptimizeMolecule(mol)

# convert to XYZ format
xyz = Chem.MolToXYZBlock(mol)
print(xyz)
```

Which gave results like:

```
40

C     4.737416    0.534657    0.261727
N     3.893546   -0.610547    0.636386
C     3.590436   -0.601056    2.076291
C     2.683899   -0.739457   -0.207159
C     1.726173    0.466581   -0.138520
O     0.591433    0.225010   -0.951940
C    -0.493159   -0.294170   -0.195691
C    -1.437545   -1.042279   -1.109406
C    -2.107114   -2.187980   -0.642047
C    -3.012057   -2.864300   -1.465734
C    -3.266874   -2.398569   -2.757733
C    -2.620964   -1.252376   -3.227052
C    -1.715000   -0.572310   -2.407587
C    -1.252406    0.818279    0.498268
C    -1.798522    0.603604    1.775959
C    -2.525708    1.613872    2.412602
C    -2.722668    2.842347    1.777145
C    -2.196315    3.061490    0.501794
C    -1.468449    2.054465   -0.139071
H     4.911214    0.547295   -0.835756
H     5.728773    0.443191    0.754382
H     4.278724    1.498670    0.571585
H     4.525284   -0.767001    2.652758
H     2.891103   -1.425149    2.334719
H     3.149765    0.367147    2.397347
H     2.136308   -1.662567    0.081630
H     2.992846   -0.888662   -1.264942
H     1.456668    0.714380    0.912866
H     2.238300    1.359934   -0.550439
H    -0.119470   -1.021104    0.565914
H    -1.931055   -2.556344    0.361048
H    -3.519544   -3.747652   -1.100170
H    -3.969047   -2.922590   -3.393201
H    -2.825368   -0.887943   -4.225484
H    -1.233055    0.319833   -2.786459
H    -1.662490   -0.345935    2.278688
H    -2.939607    1.442876    3.397958
H    -3.286822    3.622804    2.271149
H    -2.354874    4.011392    0.007879
H    -1.073775    2.240167   -1.129703
```

This step bridges the gap between chemical notation (SMILES) and computational modeling, thereby enabling the molecule to be visualized and analyzed in 3D by advanced computer applications.

### Docking in Autodock Vina through Colab

Now that I had obtained the 3D geometry, I set out to perform molecular docking simulations in a cloud environment using AutoDock Vina to predict how magnesium complexed drugs compare to the original drug with respect to BBB permeability. Opening up a new Google Colab notebook, I attempted to install AutoDock Vina using standard package commands (!apt-get install autodock-vina -y).

After about two hours of troubleshooting and reviewing the Colab and Vina manuals, I concluded that the program could not be executed successfully due to Colab limitations. This prevented docking from being completed in Colab.

### Docking in Autodock Vina through Terminal

I next tried to access Autodock Vina through my Mac OS terminal. I began by downloading AutoDock Vina 1.2.7 and confirming the installation was successful, and the application was unblocked and recognized by Terminal. This initial setup took around two hours.

I then began docking command attempts, which took a further 2-3 hours. This process involved creating using Open Babel and AutoDockTools, writing files that provide coordinates, and debugging repeated “killed” and segmentation errors. Multiple troubleshooting attempts were made (≈ 4 hours), but docking was unsuccessful.

### Docking in ORCA 5.0.4 through Terminal

I began by installing ORCA 5.0.4 (macOS Intel build) and then extracted the .tar.xz archive into `~/orca`. I verified it was active by running `~/orca/orca` and confirming I saw a valid output. I attached input files containing the 3D molecular coordinates and tried to execute the docking calculations `~/orca/orca_5_0_4_macosx10.7_intel/orca fluoxetine_mg.inp > fluoxetine_mg.out`. However, I encountered repeated runtime failures and job terminations, despite my correct syntax and file paths. After around 10-12 hours using this ORCA model, I concluded that it was not suited to carry out the needed calculations.

### Docking in ORCA 5.0.3 through Terminal

I returned to the ORCA downloads page and researched which models were capable of different tasks. I selected ORCA 5.0.3 as the ideal candidate and proceeded to download it to macOS, despite Apple's attempts to terminate each step of the process because it wasn’t scanned for viruses (this happened for each application in turn). Running the calculations for each molecule took anywhere between half an hour and two hours.

For each molecule, I opened a folder to work under:

```
mkdir ~/Documents/DiphenhydramineMg
cd ~/Documents/DiphenhydramineMg
```

And then opened a file to paste in the 3D coordinates:

```
nano diphenhydramine_mg_singlepoint.inp
```

I topped the file with:

```
! B3LYP 6-31G(d) TightSCF
%output
  Print[ P_Mulliken ] 1
end
```

And added the magnesium to the molecule:

```
Mg      0.591433      0.225010      1.200000
```

I then ran the calculation to find the complex properties:

```
~/orca/orca_5_0_4_macosx10.7_intel/orca diphenhydramine_mg_singlepoint.inp > diphenhydramine_mg_singlepoint.out
```

And organized the resulting files in Finder.

```
mv ~/DiphenhydramineMg ~/Documents/
cd ~/Documents/DiphenhydramineMg
mkdir Input Output
mv diphenhydramine_mg_singlepoint.inp Input/
mv diphenhydramine_mg_singlepoint.out diphenhydramine_mg_singlepoint_property.txt diphenhydramine_mg_singlepoint.densities diphenhydramine_mg_singlepoint.gbw Output/
```

Finishing this process for each molecule marked the completion of docking.

### PubChem Validation

To confirm the values computed for TPSA and LogP through RDKit are accurate, I compared them to real, curated data from the PubChem database. This involved selecting a single molecule (Fluoxetine) as a test case and searching for its TPSA and LogP values from PubChem’s Chemical and Physical Properties section. Then I compared it with the RDKit-computed results for the free molecules, which were found using:

```python
tpsa_free = Descriptors.TPSA(m_free)
logp_free = Descriptors.MolLogP(m_free)
```

This code output extremely similar values to those in PubChem, so I deemed the RDKit computations to be accurate and trustworthy.

### RDKit Analysis

Through Google Colab, RDKit was used to compute TPSA and LogP for each drug and corresponding analog. For the free-state molecules, the TPSA and LogP were calculated directly from the SMILES strings, while the complexed molecules were computed from the ORCA output files. Copilot assisted in structuring Python workflows, debugging descriptor calculations, and organizing the comparative DataFrame that summarized free versus complexed values. The data outputs were visualized through various plots and tables.
