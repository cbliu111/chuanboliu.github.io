---
title: "Variational principle for stochastic dynamics"
date: 2023-12-13
categories:
  - blog
tags:
  - algorithm
  - reinforcement learning
math: true
---

The variational principle for stochastic dynamics is first proposed in my paper "Error-Controlled Coarse-Graining Dynamics with Mean-Field Randomization", published in JCTC in 2023 [paper]. 
Here, we reinterpret the coarse-grain protocol as a proposal distribution which is intended to be used to approach the true trajectory distribution following the variational strategy. 

For a stochastic dynamical system with the actual law $p(\mathbf{x}(t))$, assuming another variate law $p(\mathbf{x}(t) | \mathbf{\sigma})$ with variational parameter $\mathbf{\sigma}$ that determines the degree of variation. 

The mutual information between the actual law and the variational parameter gives the average KL-divergence of the actual law and the variate law.

$I(\mathbf{x}(t), \mathbf{\sigma}) = \int p(\mathbf{x}(t), \mathbf{\sigma}) \log \frac{p(\mathbf{x}(t) | \mathbf{\sigma})}{p(\mathbf{x}(t))} D\mathbf{x}(t) d\mathbf{\sigma}$

$= \int p(\mathbf{\sigma}) \left[\int p(\mathbf{x}(t) | \mathbf{\sigma})  \log \frac{p(\mathbf{x}(t) | \mathbf{\sigma})}{p(\mathbf{x}(t))} D\mathbf{x}(t) \right] d\mathbf{\sigma}$

$= \langle D_{KL} (p(\mathbf{x}(t) | \mathbf{\sigma}) || p(\mathbf{x}(t))) \rangle_{\mathbf{\sigma}}$

$= \langle \log \omega_t \rangle_{\mathbf{x}(t), \mathbf{\sigma}}$

which is the average KL-divergence between the variate law and the actual law. 
Since KL-divergences is positively defined, when $I(\mathbf{x}(t), \mathbf{\sigma}) = 0$, then $p(\mathbf{x}(t) | \mathbf{\sigma}) = p(\mathbf{x}(t))$ regardless of the variational parameter $\mathbf{\sigma}$. 
In this case, the variate law is independent of the variational parameter. 
Therefore, the averaged importance weight provides a general variational principle for the dynamical law of stochastic dynamical systems. 

If we limit $I(\mathbf{x}(t), \mathbf{\sigma}) < \epsilon$, then $\langle D_{KL} (p(\mathbf{x}(t) \mid \mathbf{\sigma}) \Vert p(\mathbf{x}(t))) \rangle_{\mathbf{\sigma}} < \epsilon$. 
There will still be countless $\mathbf{\sigma}$ satisfy this inequality. 

Conventionally, the trajectory distribution can be sampled with the Metropolis-Hasting algorithm. 
After mixing steps, the trajectory following the true distribution can be sampled through a Markov chain with a handcraft transition kernel. 
However, the design of the transition kernel is difficult, especially when multi-modal distribution is considered. 
The transition from one mode to another can be very inefficient since the density within the intermediate region is very small. 
However, for neural network based models, the sampling is not restricted to a single mode, so the sampling is complete and efficient.

Neural network based model samples trajectories based on the internal proposed distribution, which is computational efficient due to parallel tensor operations on the GPU. 
The computational cost for one trajectory point on $n$ dimensional state space scales as $O(n^2)$ if using attention-based transformer as architecture. 
The computational cost can be reduced to $\sim O(n)$ using RNN or linear transformer variants, but with potentially decreased accuracy. 
For conventional Monte Carlo sampling, the cost is $O(1)$, which is independent of the dimensionality of the state space. 
The ideal computational cost is achieved with the price that sampling is done locally, at the cost of difficult to escape local attractive basins. 

In contrast to conventional methods, generative models facilitate rapid screening of the most probable regions within the state space. 
Because the joint distribution is automatically normalized, the computation of the partition function is obviated. 
Given that $n \approx 10^2 \sim 10^5$ in practical applications, linear or sub-linear computational costs are acceptable; indeed, robust exploration of the state space is significantly more valuable than the computational expense incurred. 
Ultimately, the computational cost is a justifiable investment for the discovery of optimal solutions.




[paper]: https://pubs.acs.org/doi/abs/10.1021/acs.jctc.3c00470





