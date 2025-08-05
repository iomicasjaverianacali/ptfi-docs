# Workflow

## Introduction

The preprediction pipeline is mainly implemented in the classes `PrePredictionWorkflow` and `PredictWorkflow`  from the file Workflow.py.

The `PrePredictionWorkflow` class implements a methodology to obtain the tandem mass spectrums from a list of experiments (MS1 scans) given in .mzML format. All the functionality of such class can be consulted in the API page for it ([Preprediction API](preprediction.md)).

The `PredictWorkflow` class implements a methodology to predict the molecular structure representation (SMILES) of a given tandem mass spectrum. Likewise, all the functionality of this class can be consulted in the API page for it ([Prediction API](prediction.md)).

On the other hand there is also functionality developed to train a Transformer-based neural network architecture to get the SMILES from the tandem mass spectrums. This training process is developed in the classes of the file `TrainWorkFlowV2.py`. All the functionality of the classes and methods used there can be consulted in [Training](training.md). 

All the functionality is available through the methods that that class implements. The specific functionality details
are specified in the API documentation.