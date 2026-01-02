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
    * random error: $P\left(|\epsilon_n| \le 1.96 \frac{\sigma}{\sqrt{n}} \right)≈0.95$
    * low coverage: hard to sample rare events
  * Numerical integration: Finite State Projection (FSP)
    * high computational/memory complexity, on order of $O(w^d)$
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

## Innovation

* For NNCME, capability demanded for representing the "discrete solution space" $(x_t, \sigma, x_0, t)$ is $O(TN^{2d}M^c)$, where $M$ is the number of points in each axis of the parameter space and $c$ is the dimension of the parameter space.
* However, real solution space is continuous, required representation capability is infinite.
* Our method: Master Equation Transformer (MET) -- representing continuous time and parameter space through incorporation of continuous-valued prompts $p(x_t, \sigma, x_0, t) = p(x_t \mid \sigma, x_0, t) p(\sigma, x_0, t)$
* Neural network with prompts:
  * a unified methodology for handling both discrete and continuous variables
  * essential information for querying the solution $x_t$ without integration or tracking of system evolution
  * enhanced generalization
  * universal architecture for representing conditional joint probability distribution
  * access solutions corresponding to different conditions simultaneous in parallel
  * train with reinforcement learning: explore the most probable sites of state space automatically
  * automatically normalization avoid computation of partition function
  * apply robustly for multi-mode systems
  * computational cost scales like $O(d^2)$
  * can be used to extrapolation of parameter space through generalized modeling capability
  * parallel trajectory ensemble sampling after training

## Significants

* Neural network with prompts is a universal architecture for representing CME solution space, both discrete and continuous variables can be handled uniformly
* Including of prompts permits the query of solutions without integration or tracking system evolution, allowing for model selection and parameter inferencing
* Automatically normalized trajectory ensemble or single-time site state sample can be simultaneously generated for different conditions in parallel, provide maximum predictability for system evolution
* Training based on discrete time or parameter dataset can be generalized to continuous time or parameter space
* For NNCME, computational complexity for solving the solution space is on the order of $O(TdM^c)$ which is only $O(Tdc^x)$ for MET with $x$ being some polynomial factor
* Capability of MET in real practice proved by GPT-4: $50257^{32768}$ with about $10^{14}$ parameters
* Encapsulation of all dynamical knowledge into a single neural network
* The power of modeling solution space + screen continuous space with polynomial computational complexity + enormous representation capability = large foundational model for stochastic dynamical systems




















[Distilling dynamical knowledge from stochastic reaction networks]: https://www.pnas.org/doi/abs/10.1073/pnas.2317422121
