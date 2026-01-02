---
title: "My work: force field reconstruction from single-cell morphology data"
date: 2024-11-13
categories:
  - blog
tags:
  - algorithm
  - my work
math: true
---

The paper is published in Adv Sci, [Quantifying the Single‐Cell Morphological Landscape of Cellular Transdifferentiation through Force Field Reconstruction]

## Motivation

* A general framework for reconstructing force field from single-cell data that lack velocity information
* A general representation and similarity measurements that can be uniformly applied to multi-omics datasets, including cell morphology
* Efficient for dealing with large-scale dataset by using machine learning algorithm
* Sampling stochastic trajectories, instead of deterministic trajectories for thermodynamics analysis
* Handling the irregularity of morphology of neural cells
* Develop a thermodynamic description of the transdifferentiation process

## Innovation

* Reconstruct the force field through score field and flow field, directly from the general stochastic dynamical equation
* Using Gromov-Hausdorff distance to quantify the similarity of cell morphology, which is robust for irregular cells
* Using sparse field reconstruction method to inferr score field and flow field
* Compute flow field by the Kramer-Moyer coefficient
* Compute score field with a mixture density model to approximate the marginal probability distribution
* The flow field is obtained through averaging over similar sample points, instead of averaging over velocities which is only valid under the assumption that similar state has similar velocity
* Including score field that reflect the constraints of marginal probability distribution, which is lacking in dynamo, causing small estimation of barrier height

## Significant

* A general algorithm and theoretical framework for analyzing multi-omic single-cell datasets
* Handling irregular cell morphology, which is not possible for previous methods, e.g. CellProfiler, Cell Painting, PhenoPlot, the morphome, cell polymorphism, CellTraj, as well as VAMPIRE and M-TRACK. 
* The same framework is generally applied to any stochastic systems, where score field and flow field can be parameterized by neural networks
* The combination of score field and flow field allows for sampling of stochastic trajectories for analyzing thermodynamics and exploration of noise strength
* The algorithm is particularly suitable for cell painting, which can reveal multi-scale single-cell morphology features and quantify the morphological landscape through the multi-scale information
* We can leverage generative neural network to design more sophasticated inference model in light of the sampling adequacy, dynamical uniformity, and Markovianity of the current method








[Quantifying the Single‐Cell Morphological Landscape of Cellular Transdifferentiation through Force Field Reconstruction]: https://advanced.onlinelibrary.wiley.com/doi/full/10.1002/advs.202512325
