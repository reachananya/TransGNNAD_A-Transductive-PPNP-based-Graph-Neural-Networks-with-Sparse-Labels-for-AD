# TransGNNAD_A-Transductive-PPNP-based-Graph-Neural-Networks-with-Sparse-Labels-for-AD

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Official implementation of "TransGNN-AD: A Transductive PPNP based Graph Neural Networks with Sparse Labels for Early Alzheimer’s Detection" (IEEE JBHI 2025).

## Overview

We present a comprehensive framework for Alzheimer’s disease (AD) classification using diffusion MRI data through multiple graph neural network architectures in a transductive learning setup. Our method, TransGNN-AD, addresses this limitation by building brain networks from tractography-derived fiber counts between regions of interest and engineering histogram-based connectivity features that effectively represent connectivity distribution patterns.  We leverage a transductive learning approach, which first project high-dimensional diffusion MRI data to compact lower-dimensional histogram-based features, which are further fed to the proposed TransGNN-AD. TransGNN-AD includes computationally efficient PPNP (Personalized Propagation of Neural Predictions) approach which decouples prediction from message propagation and leverages large neighborhood for classification.  A modularity based regularizer is further added to efficiently recover the underlying topolgical structure.

![TransGNN-AD Pipeline](images/Jbhi_2025.drawio.png)


The pipeline consists of three main stages:
1. **Preprocessing** of diffusion MRI data, including tensor fitting and deterministic tractography
2. **Feature engineering** using normalized histograms of connectivity features from 9 neuroanatomically-significant ROIs
3. **Transductive and inductive classification** using advanced Graph Neural Networks (APPNP (proposed), ARMA, ChebConv, JacobiConv) and traditional ML models (Random Forest, MLP) for CN vs MCI and CN vs AD tasks.

## Repository Structure

```
TransGNN-AD/
├── Classification/               # Classification code for CN vs MCI and CN vs AD; Traditional ML methods (Random Forest, MLP); Graph-based methods (APPNP, ARMA, ChebConv, JacobiConv)
│   ├── CN_AD/              
│   └── CM_MCI/                    
├── preprocessing_code/           # Preprocessing pipeline for diffusion MRI data
│   ├── Step1_*.py             # DICOM to NIfTI conversion 
│   ├── Step2_*.py             # Quantitative parameter extraction
│   ├── Step3_*.py             # DTI model and tractography 
│   ├── Step4_*.py             # Diffusion tensor generation
│   ├── Step5_*.py             # JHU atlas registration
│   ├── Step6_*.py             # ROI-specific parameter extraction
│   └── Step7_*.py             # Histogram feature generation
├── Dataset/                      # Sample dataset and instructions
│   └── example_subject/          # Example subject with raw data and preprocessed features
├── requirements.txt              # Package dependencies
└── README.md                     # Main documentation
```

## Installation

1. Clone this repository:
   ```bash
   git clone 
   cd TransGNN-AD
   ```

2. Create and activate a virtual environment (optional but recommended):
   ```bash
   python -m venv transGNN-AD_env
   source transGNN-AD_env/bin/activate  # On Windows, use: transGNN-AD_env\Scripts\activate
   ```

3. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```

## Data

We use diffusion MRI data from the Alzheimer's Disease Neuroimaging Initiative (ADNI) database. Due to data access restrictions, users need to apply for access to the ADNI database directly.


An example subject with the expected data structure is provided in the `Dataset/example_subject/` directory.

## Usage

### Preprocessing Pipeline

The preprocessing pipeline consists of 7 steps, with notebooks provided for each step:

1. **Convert DICOM to NIfTI**:
   ```bash
   cd preprocessing_code
   jupyter notebook Step1_preprocessing_ADNI_AD.ipynb
   ```

2. Follow subsequent steps (2-7) in order to generate the histogram features for classification.

### Classification

Available options:
- `--model`: APPNP (proposed), ARMA, ChebConv, JacobiConv, Random Forest, MLP
- `--task`: CN_vs_MCI, CN_vs_AD

## Results

1. **CN vs MCI Classification**

- APPNP with modularity loss achieves the best performance with 77.63% accuracy, 77.18% precision, and 84.97% recall (F1: 80.78%)
- Traditional baselines: Random Forest (72.56% accuracy) and MLP Classifier (72.83% accuracy)
- Graph neural networks show particular strength in recall and F1 score, which are crucial for early detection of cognitive decline

2. **CN vs AD Classification**

- APPNP with modularity loss leads with 73.29% accuracy, 70.26% precision, and 64.56% recall (F1: 67.06%)
- Traditional Random Forest achieves 67.04% accuracy but with significantly lower recall (36.14%)
- Graph-based models demonstrate superior sensitivity while maintaining balanced precision-recall trade-off

## Acknowledgments

Data used in the preparation of this article were obtained from the Alzheimer's Disease Neuroimaging Initiative (ADNI) database (adni.loni.usc.edu). As such, the investigators within the ADNI contributed to the design and implementation of ADNI and/or provided data but did not participate in analysis or writing of this report.

## License

This project is licensed under the MIT License - see the LICENSE file for details. 
