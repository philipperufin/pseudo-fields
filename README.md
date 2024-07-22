# pseudo-fields
Generating pseudo labels for satellite-based crop field delineation

This repository contains a Jupyter notebook for generating pseudo-labels from pre-trained field delineation model described in [corresponding paper](https://doi.org/10.48550/arXiv.2312.08384).

Requirements: 
- [DECODE framework](https://github.com/waldnerf/decode) FracTAL ResUNet model described in [Waldner et al. 2021](https://doi.org/10.3390/rs13112197)
- [Pre-trained model weights](https://zenodo.org/doi/10.5281/zenodo.7315089) from [Wang et al. 2022](https://doi.org/10.3390/rs14225738)

The pseudo label selection routine grounds on predictions on unlabeled data and uses an array of quality criteria including semantic confidence, instance confidence, and object size to filter high-quality predictions which can be used for weakly supervised fine-tuning of the pre-trained model architecture. 

![workflow_pseudo](https://github.com/philipperufin/pseudo-fields/assets/38853597/f5b42910-57b8-4145-8dc4-a1ab492265e6)

Our example builds on a model pre-trained in France and India, but the approach can be used for any field delineation architecture yielding pixel-level probabilities of cropland extent (for semantic confidence scores) and field boundary (basis for instance confidence scores). We use the model to identify fields in Mozambique, arguably a more complex and heterogeneous region. In our study, we find that using the 99th percentile of the semantic confidence score yields the best results, and that combining pseudo labels with human annotations results in the best performance. Pseudo labels are stored in the format needed to train the FracTAL ResUNet as described in [Wang et al. 2022](), i.e. three band raster files containing 1) cropland extent, 2) field boundaries, 3) normalized within-field distance to nearest boundary. 

Test.