# TransGNNAD_A-Transductive-PPNP-based-Graph-Neural-Networks-with-Sparse-Labels-for-AD

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Official implementation of "TransGNN-AD: A Transductive PPNP based Graph Neural Networks with Sparse Labels for Early Alzheimer’s Detection" (IEEE JBHI 2025).

## Overview

We present a comprehensive framework for Alzheimer’s disease (AD) classification using diffusion MRI data through multiple graph neural network architectures in a transductive learning setup. Our method, TransGNN-AD, addresses this limitation by building brain networks from tractography-derived fiber counts between regions of interest and engineering histogram-based connectivity features that effectively represent connectivity distribution patterns.  We leverage a transductive learning approach, which first project high-dimensional diffusion MRI data to compact lower-dimensional histogram-based features, which are further fed to the proposed TransGNN-AD. TransGNN-AD includes computationally efficient PPNP (Personalized Propagation of Neural Predictions) approach which decouples prediction from message propagation and leverages large neighborhood for classification.  A modularity based regularizer is further added to efficiently recover the underlying topolgical structure.

![TransGNN-AD Pipeline](images/Jbhi_2025.drawio.png)
