# residue-interaction-project
Residue Interaction Networks are derived from protein structures based on geometrical and physico-chemical properties of the amino acids. RING (https://ring.biocomputingup.it/) is a software that takes a PDB (https://www.rcsb.org/) file as input and returns the list of contacts (residue-residue pairs) and their types in a protein structure. RING contact types include:

●	Hydrogen bonds (HBOND)
●	Van der Waals interactions (VDW)
●	Disulfide bridges (SBOND)
●	Salt bridges (IONIC)
●	π-π stacking (PIPISTACK) 
●	π-cation (PICATION)
●	Unclassified contacts

we developed a software that can predict the RING classification of a contact based on statistical or supervised methods, rather than geometrical constraints. The program should is able to calculate the propensity (or probability) of a contact belonging to each of the different contact types defined by RING, starting from the protein structure.
I developed the AI predictor and my collegue modified a repository of codes and created the command cotrol launcher of the software
