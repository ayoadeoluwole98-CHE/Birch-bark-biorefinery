# Design basis (v0.1)
## 1. Objective and scope: Design a process plant for the production of betulin, and suberin from outer birch bark. 
The process will start with already crushed and fine outer birch bark (< 2 mm particle size). 
The design will be done in DWSIM, and the P&ID will be drawn in draw.io. Analysis and conditional optimisation will be done with python

## 2. Feed specification: 
The feeds are birch bark, ethanol-water mixtures, and sodium hydroxide at different stages. Some extractive solvents might also be considered.
Feed composition will be denoted in DWSIMS simulation by specificying each component. Betulin, suberin, soluble Phenols&Sugars, and residue.

#Feed composition of the outer birch bark, from literature (reference 3), <1.5mm particle size, and ambient condition.
feed_comp = pd.DataFrame({"86wt% dry(%)":[37.0, 38.0, 13.4, 5.8, 3.4, 2.4] }, 
                         index=["Betulin", "Suberin", "Lignin", "polysaccarides", "Cellulose", "Others"])
feed_comp.sort_values("86wt% dry(%)", ascending=False)


Component	Represents	Notes
Betulin:	The main product	A real compound (C₃₀H₅₀O₂, molar mass about 442.7 g/mol, melting point roughly 250-260°C), so you can use literature properties
Suberin (lumped):	The polyester in the bark	One pseudo-component, or 2-3 representative monomers, such as 22-hydroxydocosanoic acid (C₂₂H₄₄O₃, about 356.6 g/mol) and octadecanedioic acid (C₁₈H₃₄O₄, about 314.5 g/mol)
Residual bark solids:	Cellulose, lignin, and other insoluble material	Lumped, with an assumed molar mass
Polyphenols + sugars:	The co-extractives treated as waste	Lumped into one component

Water, ethanol, glycerol, NaOH, HCl, and NaCl are most likely already in the database.

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

Extractive: Phenols and Sugars. Phenols can be extracted with washing water, 
at later stage, which is used as a side stream  for wastewater treatment in this project.
Literature data (Kuznetsov et al., 2005) (isopropanol extraction, used as a proxy for ethanol) indicate
that extractives stands at about 40% of the bark. Water-soluble extractives like the Polyphenols and sugars are treated as waste: they remain in the mother liquor after betulincrystallization and leave the process with the aqueous bottoms of the solvent 
recovery column. Only the distilled ethanol is recycled.

## 4. Process route summary (from laboratory procedure)
1. Bark is dried (60 °C) and milled to < 1.8 mm.
2. Bark is contacted with ethanol:water (9:1) at 8 mL/g, 90 °C, in a
   closed reactor with NaOH (20 wt% of dry bark), 60 min.
3. The hydrolysate is drained, the residue washed with ethanol:water
   (1/3 of original volume, 80 °C), and the liquors combined.
4. Ethanol is evaporated and recycled. The residue is mixed with boiling
   water; betulin precipitates, is filtered and dried.
5. The aqueous filtrate containing suberin salts is acidified with 2 M HCl;
   suberin acids precipitate, are filtered, washed and dried (70 °C).
Laboratory yields (outer bark): betulin 20.5%, suberin 26.1% of the feed weight.

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
1. https://www.sciencedirect.com/science/article/pii/S0959652624030191#bib24
2. https://www.mdpi.com/1420-3049/24/23/4391
3. https://www.sibran.ru/upload/iblock/4b9/improvement_of_excretion_methods_and_studying_the_composition_and_properties_of_birch_bark_extracts.pdf
