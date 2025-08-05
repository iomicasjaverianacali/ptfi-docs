# Using fragmentation trees and mass spectral trees for identifying unknown compounds in metabolomics

## Introduction 

The Metabolomics Standards Initiative (MSI) categorizes structure elucidation into four different levels: 

- Identification
- Annotation
- Characterization
- Classification

However, MSI does not provide a scoring schema to rank identified compounds within the identified and annotated categories, a caveat that was recently highlighted by metabolomics investigators.

Identification of metabolites refers to complete identification of the structure, including molecular connections and **stereochemical assignments**.

Some major differences between metabolomics and proteomics are the presence of **multiply-charged ions** from peptides and the much larger chemical diversity in metabolomics and **exposome** analyses.

**Structure annotations** are often ambiguous due to the large number of possible isomers, data inaccuracies, limited amounts of corroborating information, and human errors, including misclassification of sub-structures.

However, annotation can also be viewed as a strategy to reduce the need for **isolation of compounds** and de-novo elucidation. 

The idea is to annotate mass spectra using the most probable elemental compositions found in public databases and to add additional **orthogonal filters** to decrease the number of **structure hits**.

Computer-assisted structural elucidation (CASE) encompasses structural dereplication using various analytical techniques like tandem MS (MS2).

Essentially, dereplication is a process to identify “known unknowns”, which are compounds that are unknown at the time of detection and with further investigation are then found to be known compounds

CASE first reduces chemical and spectral properties of an unknown compound, second generates candidate structures compatible with spectral features, and then ranks these candidates.

CASE can be used when manual interpretation of data is impractical and outcomes are unreliable using certain techniques, such as artificial intelligence, pattern recognition, library search, and spectral simulation.

Both structural dereplication and CASE are not considered de-novo identification because they rely on database searches with pre-existing known metabolites or reference standards.

Full de-novo identification by MS alone can hardly be achieved because **isomers** are difficult to distinguish by MS.

Mass spectral data inform about **elemental compositions** by combining accurate mass and isotopic information.

Collision-induced fragmentation data on the MS2 or MSn levels are used to find structural information from unique fragmentation patterns to test for the presence and the absence of functional groups.

## Trees

Typically, the graphs are called fragmentation trees, family trees or identification trees, if these trees show the fragmentation pathway of a molecule.

Fragmentation trees are generated computationally to predict the **fragmentation pathway** of a molecule.