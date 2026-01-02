---
title: "My work: Coarse-graining sampling"
date: 2023-10-31
categories:
  - blog
tags:
  - algorithm
  - my work
math: true
---

The paper is published in JCTC, [Error-Controlled Coarse-Graining Dynamics with Mean-Field Randomization]. 

## Motivations

* Chemical reaction systems have intrinsic high-dimensional state space $S \in \mathbb{R}^d$, solving chemical master equation is challenging. 
* Common methods and computational complexities:
  * Kinetic Monte Carlo $O(dn)^{1/2}$, convergence demands typically $n \approx 10^4 \sim 10^7$ trajectories, with random error $P\left(\lvert \epsilon_n \rvert \le 1.96 \frac{\sigma}{\sqrt{n}} \right)≈0.95$
  * Finite state projection $O(w^d)$, error $P(x \in X_w) \le \epsilon$
* Delbrück-Gillespie process, a consistent theoretical framework: 
  * Reaction rate equation, Ludwig Wilhelmy, 1850s
  * Discrete-stochastic behavior of a chemically reacting system, Delbrück, 1940
  * Exact stochastic simulation algorithm, Gillespie, 1976
  * Chemical Langevin equation, Gillespie, 2000
  * 𝜏-leap algorithm, Gillespie, 2001
* From microscopic through mesoscopic to macroscopic, an informative error of coarse-graining the stochastic dynamics 
* A uniform perspective of stochastic process uniformization, 𝜏-leap and rejection-based algorithms
* A dynamic renormalization method to rescale both the state space and time 
* Scale-independent trajectory sampling algorithm

## Mean-field randomization

* Uniformization (virtual reaction): $a_{K+1}(X(t)) = \bar{a} - \sum_k a_k(X(t))$
* $\tau$-leap: $a_j(X(t)) = \bar{a}$ for $t \in (t, t+\tau)$
* Rejection-based: $a_j(X(t)) = \bar{a}$ for $X(t) \in [X - \delta X, X + \delta X]$
* Our method, mean-field randomization: $a(x; x \in \Gamma(x)) = \hat{a}$, $\hat{a} = \frac{1}{\Gamma_x} \int_{\Gamma(x)} a(x) dx$
  * transforms the state space into a reduced sparse space
  * mesostate is integration of microstates
  * intrinsic-time distribution becomes invariant within the mesostate
  * preservation of Markovian renewal properties: $p(x_{i+1}; t_{i+1} \mid x_i; t_i, \ldots, x_0; t_0, \Gamma(x_0)) = p(x_{i+1}; t_{i+1} \mid x_i; t_i, \Gamma(x_0))$, $p(\Gamma(x_{n+1}; t_{n+1}) \mid \Gamma(x_n; t_n), \ldots, \Gamma(x_0; t_0)) = p(\Gamma(x_{n+1}; t_{n+1}) \mid \Gamma(x_n; t_n))$

## Resampling the fine-scale dynamics from coarse-scale dynamics

* Recovery of exact dynamics through rejection sampling: $x_{CG}(t) = x(0) + \sum_j Y_j \left( \int_0^t \hat{a}\_j(x, \tau) d\tau \right) v_j$, $B\left[ Y_j \left( \int_0^t \hat{a}\_j(x(s), s) ds \right) \right] = \lim_{L \to \infty} \sum_{l=0}^{L-1} B_l \left[ Y_j(\hat{a}\_j(t_l) \Delta t_l \right] = \lim_{L \to \infty} \sum_{l=0}^{L-1} Y_j(a_j(t_l)\Delta t_l) = Y_j \left( \int_0^t a_j(x(s), s) ds \right)$, $\hat{x}(t) = x(0) + \sum_j B\left[ Y_j\left( \int_0^t \hat{a}_j(x, \tau) d\tau \right) \right] v_j$
* Recovery of exact dynamics through importance sampling: $\hat{p}(x_0, x_f; t) = \frac{1}{n} \sum_i \omega_t^{(i)} I_{x(t) = x_f}$, $\omega_t^{(i)} = \frac{p[x_{(0, t] \mid x_0}]}{q[x_{(0, t]}^{(i)} \mid x_0]}$

## Informative error of coarse-graining

We quantify the error by mutual information between coarse-graining dynamics and the coarse-graining procedure

$I[x_{(0, t]}, \Theta] = \sum_\Gamma KL(q[x_{\Delta t_\Gamma}] \Vert q[x_{\Delta t_\Gamma}]) = \sum_\Gamma E_q[\ln \omega_{\Delta t_\Gamma}] = E_q[\ln \omega_t]$

The result is nothing else but the expectation of the logarithm importance sampling weight. Expansion: first term is trivial 0, and second term gives the $\chi^2$ distribution divergence. $E_q[\omega_t] = 1$, $E_q[(\omega_t -1)^2] = \int \left( \frac{p[x_{(0, t]}]}{q[x_{(0, t]}]} -1 \right)^2 q[x_{(0, t]}] Dx_{(0, t]}$. 

Control coarse-graining error by step-wise weight, the error-controlled coarse-graining dynamics sampled by mean-field randomization ($\omega$-leap) has the minimum computational time in all error range. 

## Scale-independent trajectory ensemble sampling

Coarse-graining dynamics sampled using mean-field randomization dependents on the number of mesostates instead of the number of microstates. 
If propensity functions are approximately linear with state variation, number of mesostates is approximately invariant with respect to scale expansion. 
Hence, scale-independent sampling of trajectory ensemble is possible. 

## Significants

* Dynamic renormalization on both state space and time
* Randomization: mesostates are not static
* Uncorrelated reaction events and disentangled joint probability distribution, similar to mean-field approximation method in statistical physics
* Error of coarse-graining dynamics is controlled by informative bound
* Almost invariance number of mesostates as system scale expansion
* Up to 10^4-fold simulation accelerations
* The method can be potentially applied to complex systems to comprehend the multiscale behavior under informative error control, coarse-grain dynamics at different emergent levels are then corresponding to mesostates of different scales

[Error-Controlled Coarse-Graining Dynamics with Mean-Field Randomization]: https://pubs.acs.org/doi/abs/10.1021/acs.jctc.3c00470





