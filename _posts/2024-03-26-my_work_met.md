---
title: "My work: neural network modeling of complex systems"
date: 2024-03-26
categories:
  - blog
tags:
  - algorithm
  - my work
math: true
---

The paper is published in PNAS, [Distilling dynamical knowledge from stochastic reaction networks]

## Motivations

* Complex systems in open environment across diverse domains can be modeled by Chemical Master Equations (CMEs)
* Methodologies of solving CME and drawbacks:
  * Trajectory sampling: Kinetic Monte Carlo
    * slow convergence: typically $10^4 \sim 10^7$ trajectories to estimate the joint probabilities
    * random error: 𝑃(〖|𝜖〗_𝑛 |≤1.96 𝜎/√𝑛)≈0.95
    * low coverage: hard to sample rare events
  * Numerical integration: Finite State Projection (FSP)
    * high computational/memory complexity, on order of 𝑂(𝑤^𝑑)
    * low state space exploration
    * hyper-parameter sensitive
  * Low-rank representation: Tensor-networks (TN)
    * scalability issue: contraction of large TN is computationally intensive and memory-hungry
    * universality issue: lack of universal network structure for all type of problems
    * dynamic range and sparsity issue: wide dynamic range or dense tensor structure cause computational inefficiency
  * Neural network: mixture-density network (MDN), Neural-Network Chemical Master Equation (NNCME)
    * training dataset problem: sampling training data is time consuming and system-specific
    * partial representation: only marginal (MDN) or discrete-time distributions (NNCME) are considered
    * narrow application: hard to be used in downstream computations
* Lack of a general method for model parameters inferencing for large systems
* Application of the universal approximation and generalization powers of neural networks in understanding scientific problems
* The representation power of neural networks is invaluable for describing complex systems involving many interaction components
* Empower generative neural networks for error-explicit modeling and trajectory prediction
* A large language model like foundational model for complex systems

















[Distilling dynamical knowledge from stochastic reaction networks]: https://www.pnas.org/doi/abs/10.1073/pnas.2317422121
