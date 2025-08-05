# Training 

## Data 

The data available for the training process can be consulted in *placeholder for the actual place*. 

The sources of data are two:

- MassSpecGym dataset (available at [MassSpecGym dataset](https://huggingface.co/datasets/roman-bushuiev/MassSpecGym/tree/main))
- The TeFT paper dataset (available at [TeFT](https://github.com/thumingo/TeFT/tree/main/Dataset))

A statistical description of the MassSpecGym dataset is available at the page of its paper [MassSpecGym paper](https://arxiv.org/html/2410.23326v1). 

Both datasets provide both the tandem mass spectrums and Simplified Molecular Input Line Entry System (SMILES). However, the TeFT dataset does not provide intensities for its spectrums, only the mass-to-charge ratios. Besides that, the TeFT dataset does not provide any additional metadata (i.e. ion mode, energy level, etc.).


## Architecture

The base architecture for the task of predicting SMILES from tandem mass spectrums is a vanilla transformer. Modifications of it are (for now) implemented in the `v2` and `experimental` branches of the repository. The transformer architecture makes use of an encoder-decoder structure. Modifications in those branches are mainly done in the encoder part and in the attention mechanism. 

There are experimental architectural changes as well (in the `v2` branch) for training multiple tasks, namely: the main prediction task (SMILES from tandem mass spectrums), and a secondary task in charge of the prediction of the mass of the precursor. Also have in mind that custom loss functions, beyond the CrossEntropy, are also defined (in the main branch under the `RegByMassCrossEntropy` class in the `TrainWorkFlowV2.py` file) to try to force the predictions to match the precursor mass of the training tandem mass spectrums precursors.
