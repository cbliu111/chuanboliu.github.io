---
title: "Optimal transport problem. part I"
date: 2024-11-13
categories:
  - blog
tags:
  - algorithm
  - field inference
math: true
---

## Exact OT problem
Kantorovich's optimal transport (OT) problem search for a deterministic transportation plan $\pi^\*(x_1 \mid x_0)$ that satisfy 

$\pi^\* = \inf_{\pi \in \Pi(q_0, q_1)} \int c(x_0, x_1) d\pi(x_0, x_1)$

where $\Pi(q_0, q_1)$ is the set of admissible transport plans (exact arrangement).  
$c(\cdot, \cdot)$ is the ground cost, the most typical case, and the case considered here, is the quadratic form $c(x_0, x_1) = \frac{1}{2} \lVert x_1 - x_0 \rVert^2$. 

## Entropic regularized OT problem
The entropic regularized OT (EOT) problem relaxes the deterministic plan with a stochastic map $\pi^\*(x_1 \mid x_0)$, and the OT problem can be viewed as the special case of $\delta$ distribution 

$\pi^\* = \inf_{\pi \in \Pi(q_0, q_1)} \int \frac{1}{2} \lVert x_1 - x_0 \rVert^2 d\pi(x_0, x_1) - \sigma^2 H(\pi) = \sigma^2 D(\pi \mid Q_{0, 1})$

where $\Pi(q_0, q_1)$ is the set of all possible transport plans (joint distributions over $x_0$ and $x_1$ whose marginals are $q_0$ and $q_1$ in which $x_0$ and $x_1$ are independent).
$H(\pi) = \int_{\mathcal{X}} \ln \pi d\pi$ is the entropic term, and $D(\pi \mid Q_{0, 1})$ denotes the distance measure of the mapping given the marginal condition $Q_{0, 1}$. 
$\sigma$ is the regularization parameter which measures the stochasticity of the mapping, when $\sigma \to 0$, we recover the exact OT transport plan. 
EOT has a unique solution due to the strict convexity of $H(\pi)$. 

This formula is equivalent to the dynamical form {chenRelationOptimalTransport2016}

$\inf_{\rho_t, u_t} \int_\mathcal{X} \int_{0}^{1} \frac{1}{2} \lVert u_t(x) \rVert^2 d\rho_t(x) dt$

$\partial_t \rho_t + \nabla \cdot (u_t \rho_t) = 0$

$\rho(0, x) = q_0(x), \rho(1, x) = q_1(x)$

The entropic term $H(\pi)$ is zero since the trajectory is deterministic. 

## Schr\"odinger bridge and EOT
Schr\"odinger bridge (SB) with Wiener prior is about to search for the optimal path measure $P^u$ of a stochastic process $\{X_t^u\}$

$dX_t^u = u(t, X_t^u) dt + \sigma dW_t, \quad X_0^u \sim q_0$

with marginal conditions $P_0^u = q_0, P_1^u = q_1$, that is most close to the Wiener process measure $Q$:

$u^\* = \mathop{\mathrm{arg\,inf}}\_{u} KL(P^u \mid Q), \quad dQ_t = \sigma dW_t, \quad Q_0 = q_0$

By Girsanov's theorem {sarkkaAppliedStochasticDifferential2019} 

$KL(P^u \mid Q) = \frac{1}{\sigma^2} \mathbb{E}\_{P^u}\left[ \int_{0}^{1} \frac{1}{2} \lVert u_t(X_t^u) \rVert^2 dt \right]$

The time-marginals $\{\rho_t\}\_{t \in [0, 1]}$ of this process satisfy the Fokker-Planck equation {riskenFokkerPlanckEquationMethods1996}

$\partial_t \rho_t + \nabla \cdot (u_t \rho_t) - \frac{1}{2} \sigma^2 \Delta \rho_t = 0, \quad \rho_0 = q_0$

Therefore, the SB problem is reformulated as 

$u^\* = \inf_u \int_{0}^{1} \int_{\mathcal{X}} \frac{1}{2} \lVert u_t(x) \rVert^2 d\rho_t(x) dt$

s.t.

$\partial_t \rho_t + \nabla \cdot (u_t \rho_t) - \frac{1}{2} \sigma^2 \Delta \rho_t = 0, \quad \rho_0 = q_0, \quad \rho_1 = q_1$

The Reciprocal Property {leonardReciprocalProcessesMeasuretheoretical2014}chenStochasticControlLiaisons2021}{shiDiffusionSchrodingerBridge2023} of SB indicates the minimization objective $KL(P^u \mid Q)$ can be decomposed to be 

$KL(P^u \mid Q) = D(P_{0, 1}^u \mid Q_{0, 1}) + \int_{\mathcal{X} \times \mathcal{X}} \int_{0}^{1} KL(P_t^u(\cdot \mid x_0, x_1) \mid Q_t(\cdot \mid x_0, x_1)) dt dP_{0, 1}(x_0, x_1)$

where $P_{0, 1}^u$ is the joint distribution on $t=0$ and $t=1$ induced by the process $X_t^u$. 
L\'eonard et al. {leonardReciprocalProcessesMeasuretheoretical2014} proved for the optimal path measure $P^\*$ we have 

$P_t^\*(\cdot \mid x_0, x_1) = Q_t(\cdot \mid x_0, x_1), \quad (x_0, x_1) \sim P^\*_{0, 1}-a.s.$

In other words, the marginal-conditioned measure of optimal path $P_t^u$ is a Brownian bridge 

$P_t^\*(\cdot \mid x_0, x_1) = Q_t(\cdot \mid x_0, x_1) = \mathcal{N}(\cdot \mid (1-t)x_0 + tx_1, \sigma^2 t(1-t)I)$

And the SB problem is reduced to 

$KL(P^\* \mid Q) = D(P_{0, 1}^\* \mid Q_{0, 1})$

for the optimal path measure, which has the same solution as EOT by assigning $\pi^\* = P_{0, 1}^\*$. 
Therefore, SB problem is equivalent to the EOT problem 

$P_{0, 1}^\* = \pi^\* = \mathop{\mathrm{arg\,inf}}\_{\pi \in \Pi(q_0, q_1)} \int \frac{1}{2} \lVert x_1 - x_0 \rVert^2 d\pi(x_0, x_1) - \sigma^2 H(\pi)$

$P_t^\*(\cdot \mid x_0, x_1) = Q_t(\cdot \mid x_0, x_1), \quad (x_0, x_1) \sim P^\*_{0, 1}$

The optimal path measure is obtained by integral 

$P_t^\*(x) = \int P_t^\*(x \mid x_0, x_1) dP_{0, 1}^\*$

which is an infinite mixture of Brownian bridges weighted by an EOT plan. 






