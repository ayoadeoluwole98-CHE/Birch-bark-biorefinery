# Design basis (v0.1)
## 1. Objective and scope: Design a process plant for the production of betulin, and suberin from outer birch bark. 
The process will start with already crushed and fine outer birch bark (< 2 mm particle size). 
The design will be done in DWSIM, and the P&ID will be drawn in draw.io. Analysis and conditional optimisation will be done with python

## 2. Feed specification: The feeds are birch bark, ethanol-water mixtures, and sodium hydroxide at different stages. Some extractive solvents might also be considered(TBD)

## 3. Product specifications: 
Betulin: Betulin is a naturally occurring pentacyclic triterpene alcohol (white powder/crystal) found in birch bark.

Chemical Identification

• CAS Number: 473-98-3
• Molecular Formula: C₃₀H₅₀O₂
• Molecular Weight: 442.72 g/mol
• Synonyms: Betulinic alcohol, Betulinol, Betulol, Trochol, NSC 4644
• Structure: Pentacyclic triterpene with a lupane skeleton and two hydroxyl groups

Suberin is a natural, lipophilic biopolymer found in plants, primarily in bark, cork, and root tissues, known for forming waterproof barriers. 
Its structure includes a dual-domain heteropolymer with a poly(aliphatic) and a covalently linked poly(phenolic) domain, composed of long-chain 
fatty acids and hydroxycinnamic acids such as ferulic acid. Elementally, it consists of approximately 68% Carbon, 9.76% Hydrogen, and 20.66% Oxygen. 
Suberin's physical characteristics include a melting point range of 55 °C to 75 °C; its molecular weight is indeterminate in its native state but 
can be assessed in solubilised forms, with averages between 385 and 2,000 g/mol. It remains insoluble in water and other solvents unless chemically modified through processes like alkaline methanolysis.

Extractive(TBD)

## 4. Process route summary (TBD)
## 5. Operating assumptions (TBD)
## 6. Simulation tools and thermodynamic approach

- Software: DWSIM (steady state and dynamic), Python (SciPy, NumPy, Matplotlib).
- Property package: NRTL for the ethanol-water-extractives liquid phase,
  chosen because it represents the ethanol-water azeotrope.
- Custom components (betulin, suberin monomers): properties taken from
  literature where available, otherwise estimated by group contribution (Joback).
- Solid-liquid behaviour (extraction, crystallization): not predicted by the
  simulator. Solubility is modelled with an Apelblat-type correlation fitted
  to literature data in Python and imposed on the flowsheet as specified splits.
- Saponification: modelled as a conversion reactor, with no rigorous
  electrolyte thermodynamics.
  
## 7. Known data gaps
1. Betulin physical properties are not in the DWSIM database. They will be
   estimated by group contribution and marked "estimated" in data/properties.csv.
2. Betulin solubility data in ethanol-water is limited. A correlation will be
   fitted to the available points and results shown as a sensitivity range.
3. Betulin binary interaction parameters are unavailable and will be
   estimated or set to zero, as a stated limitation.
4. Suberin is a polyester mixture. We will represent it as 2-3 monomers.

## 8. References
https://www.sciencedirect.com/science/article/pii/S0959652624030191#bib24
https://www.mdpi.com/1420-3049/24/23/4391
