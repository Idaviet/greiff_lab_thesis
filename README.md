# Machine Learning Analysis of BCR Repertoires for Antibody Discovery

Master's thesis project conducted at the [Greiff Lab](https://greifflab.org/), Karolinska Institutet / KTH Royal Institute of Technology / Stockholm University.

## Overview

This repository contains code and analysis workflows from a Master's thesis investigating whether deep neural networks (DNNs) can recover structural and biochemical information from antibody sequences through dimensionality reduction analysis of integrated gradients.

The study analyzed an experimentally derived anti-HER2 CDRH3 library of >34,000 sequences classified as binders or nonbinders. Key findings include:

- **Structural recovery**: High degree of structural overlap in isolated UMAP/PCA-based clusters derived from integrated gradients, confirmed through SPACE2 structural clustering
- **Sequence diversity**: Analysis demonstrates that DNN models transcend raw sequence input in their classification strategies, with high sequence diversity maintained within reduction clusters
- **Physicochemical patterns**: Evidence suggests recovery of additional information beyond structure, potentially related to residue biochemical properties

Key components of this repository:
- **SPACE2 integration**: Structural clustering of predicted CDRH3 models to identify structural configurations
- **Dimensionality reduction optimization**: PCA and UMAP parameter tuning for integrated gradients visualization
- **Diversity analysis**: Sequence and physicochemical property assessment within reduction clusters


### Repository Structure
```plain text
Greiff_lab_Thesis/
├── SPACE2 Module/           # SPACE2 structural clustering implementation
│   ├── SPACE2/              # Core SPACE2 package
│   ├── setup.py             # Installation script
│   └── README.md            # SPACE2 documentation
├── jupyter scripts/         # Analysis notebooks
│   ├── PCA Optimization/    # PCA parameter tuning and analysis
│   ├── UMAP Optimization/   # UMAP hyperparameter optimization
│   ├── SPACE2 Analysis/     # SPACE2 clustering workflows
│   ├── Misc/                # Additional exploratory analyses
│   └── Incomplete/          # Work in progress
├── python functions/        # Reusable Python modules
└── README.md
```

### SPACE2 Module

SPACE2 (Structural Profiling of Antibodies to Cluster by Epitope 2) clusters antibodies based on structural similarity of their predicted models. Antibodies with similar CDR loop structures often bind the same epitope.

#### Installation

```bash
cd "SPACE2 Module"
pip install -e .
```
### Requirements
* Python 3.8+
* NumPy
* Pandas
* Scikit-learn
* Biopython
* [ImmuneBuilder](https://github.com/brennanaba/ImmuneBuilder) (for structural model generation)

### Usage
```python
from SPACE2 import cluster_structures

# Cluster antibody models from a directory
results = cluster_structures(
    pdb_dir='./antibody_models/',
    rmsd_threshold=1.25,
    method='agglomerative'
)

# Results contain cluster assignments
print(results[['ID', 'cluster_by_length', 'cluster_by_rmsd']])
```
For detailed SPACE2 documentation, see [SPACE2 Module/README.md.](https://ellydee.ai/chat/SPACE2%20Module/README.md)

## Analysis Workflows
### PCA Optimization
Notebooks for optimizing principal component analysis on BCR sequence features.

```bash
jupyter notebook "jupyter scripts/PCA Optimization/"
```
### UMAP Optimization
Hyperparameter tuning for UMAP dimensionality reduction on repertoire data.

Key parameters explored:
  * **n_neighbors**: Local neighborhood size
  * **min_dist**: Minimum distance between points
  * **metric**: Distance metric for high-dimensional space

### SPACE2 Analysis
End-to-end workflows for:
  1* Generating antibody structural models (ImmuneBuilder)
  2* Clustering by structural similarity (SPACE2)
  3* Epitope inference from cluster assignments

## Dependencies
```plain text
numpy>=1.21.0
pandas>=1.3.0
scikit-learn>=1.0.0
biopython>=1.79
matplotlib>=3.4.0
seaborn>=0.11.0
umap-learn>=0.5.0
jupyter
```

install all dependencies
```bash
pip install -r requirements.txt
```

## Background
### The Antibody-Antigen Recognition Problem

Antibody-antigen interactions are fundamental to the immune response, with an estimated 10^12 unique antibodies playing critical roles in immune recognition. The CDRH3 region (heavy-chain complementarity determining region 3) contributes the strongest effects on an antibody’s binding capacity. However, with only ~7,000 antibody-antigen complexes resolved experimentally at the atomic level, structural and affinity data remains extremely limited given the vast diversity of possible CDRH3 sequences (20^10 possible sequences).

### Deep Neural Networks for Paratope Prediction

Recent advances in DNNs have enabled models capable of identifying paratope sequences as potential binders to a given epitope. However, these models retain an inherent “black box” quality, making it difficult to understand the underlying logic behind their binder/non-binder classifications.

### Integrated Gradients Analysis

Integrated gradients (IG) quantify the importance of each input feature in a model’s decision-making process. Analysis of IG values from DNN classifiers has demonstrated the ability to recover structural information from raw CDRH3 sequences through dimensionality reduction techniques.

### Dimensionality Reduction for Pattern Discovery
By applying PCA and UMAP to integrated gradients, this study sought to:

* Identify clusters of sequences with similar IG profiles
* Determine whether these clusters correspond to structural similarities
* Assess whether models recover information beyond raw sequence (e.g., physicochemical properties)
* Validate methodology on experimentally derived (vs. synthetic) antibody sequences

### SPACE2 for Structural Clustering
SPACE2 clusters antibodies based on structural similarity of predicted models. In this study, SPACE2 was applied to CDRH3 structural predictions to:
* Identify distinct structural configurations within reduction clusters
* Compare structural diversity between binder and non-binder groups
* Assess whether dimensionality reduction clusters correspond to structural similarity

## Citations
If you use SPACE2, please cite:
```Bibtex
@article{Spoendlin2023,
  title = {Improved computational epitope profiling using structural models identifies a broader diversity of antibodies that bind the same epitope},
  author = {Fabian C. Spoendlin, Brennan Abanades, Matthew I. J. Raybould, Wing Ki Wong, Guy Georges, and Charlotte M. Deane},
  journal = {Frontiers in Molecular Biosciences},
  doi = {10.3389/fmolb.2023.1237621},
  volume = {10},
  year = {2023},
}
```

## Author
**Isaac G.L. Daviet**
M.Sc. Molecular Techniques in Life Sciences
Karolinska Institutet / KTH Royal Institute of Technology / Stockholm University
* GitHub: [@Idaviet](https://github.com/Idaviet)
* [LinkedIn](https://www.linkedin.com/in/isaac-daviet)

## Acknowledgements
[The Greiff Research Group](https://greifflab.org/), in particular Rahmad Akbar, Robert Frank & Victor Greiff for supervision and resources
