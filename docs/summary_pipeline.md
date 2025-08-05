# Pre-prediction



# Prediction

The following is a diagram of how the pipeline proceeds after the Pre-prediction step.

<figure markdown="span">
  ![Image title](/docs/assets/pipeline_prepredict.png){ width="300" }
  <figcaption>Pipeline after preprediction</figcaption>
</figure>

1. There are available $N$ experimental tandem mass spectrums (denoted by $MS$) $\left{ MS_{i}\right}_{i=1}^{N}$.

2. For each $MS_{i}$, $M$ SMILES (denoted by $S$) are predicted, giving groups: $MS_{1} \rightarrow \left{ S_{1i} \right}_{i=1}^{M}$, $MS_{2} \rightarrow \left{ S_{2i} \right}_{i=1}^{M}$, ..., $MS_{N} \rightarrow \left{ S_{Ni} \right}_{i=1}^{M}$

2. For each of the $M$ SMILES (associated to an experimental mass spectrum) a computational mass spectrum (denoted by $P$) is predicted, thus giving $S_{ij} \rightarrow P_{ij}, \: \: i=1,...,M \and j=1,...,N$

3. Each of these $P$ are transformed into a new representation (new vector) by using an embedding transformation (using the methodologies described in DreaMS), so that for a given $j$, the $P_{ij}_{i=1}^{M}$ can be compared with its $MS_{j}$ in these new represantations, using any available similarity metric. Cosine similarity is used as the default metric.

4. The highest similar $P_{kj}$ from the previous step (with $k$ being the index of the highest similar spectrum) is chosen as the most likely computational spectrum to resemble the original spectrum $M_{j}$, and therefore its associated SMILES $S_{ik}$ is also chosen as the most likely SMILES associated to that spectrum $M_{j}$