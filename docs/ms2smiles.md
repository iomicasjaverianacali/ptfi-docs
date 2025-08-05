# De novo molecular structure generation from mass spectra

Metabolomics: small molecule identification from biological samples

Approaches used in identification of unknown molecules:

- Search a mass spectral library to find molecular structures that may potentially match the unidentified mass spectra
- Use tools like MetFrag, CFM-ID, SIRIUS to predict **molecular fingerprints** based on the mass spectra. Then, the fingerprints are also compared to the ones already calculated and stored in a database to determine potential matches,

## Other frameworks

- MSNovelist predicts small molecule structures using MS data, departing from
traditional database searches and comparisons

## Challenge

One key challenge is the implicit inclusion of hydrogen atoms, which, if overlooked, can lead to incorrect molecular formula corresponding to the generated SMILES.

To overcome this, MS2SMILES predicts both heavy atoms and their associated hydrogen atoms as a single unit. 

Additionally, molecular fingerprint and formula convey distinct information, and to leverage both effectively, MS2SMILES incorporates a learnable parameter to enhance their combined impact.

## Results

- Validated on GNPS.

- It correctly predicted 27.5%, 41.0%, and 45.1% of SMILES at top 1, top 5, and top 10, respectively.

