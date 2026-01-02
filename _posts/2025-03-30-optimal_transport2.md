---
title: "Optimal transport problem. part II"
date: 2025-03-30
categories:
  - blog
tags:
  - algorithm
  - field inference
math: true
---

## Entropic unbalanced OT problem

Entropic Unbalanced Optimal Transport (EUOT) further relaxes the marginal constraints using the f-divergence $D_{\Psi}(\mu|\nu) = \int \Psi(\frac{d\mu}{d\nu})d\nu$ as the average Radon-Nikodym derivative of two measures. 
And $\Psi: [0, \infty) \to [0, \infty]$ is assumed to be a convex, lower semi-continuous, non-negative function and $\Psi(1) = 0$, i.e. identical measure has zero divergence. 
We assume $\Psi$ is an differentiable entropy function that satisfy superlinearity, i.e. $\Psi^{'}_\infty := \lim_{x \to \infty} \Psi(x)/x = \infty$. 
Superlinearity means the growth of $\Psi$ is faster than linear as $x \to \infty$. 
Therefore, we ensured $D_{\Psi}(\pi_1\mid q_1) = \infty$ when $\pi_1$ has singularity with respect to $q_1$, i.e. when $\pi_1(A) = 1$ and $q_1(A) = 0$ for some set $A$. 
Also, due to the superlinearity, continuity and convexity of $\Psi$, $D_\Psi$ is a lower semi-continuous function, as desired by the EUOT problem. 
Formally, we have 

$\pi^\* = \inf_{\pi \in \mathcal{P}\_2(\mathcal{X} \times \mathcal{X})} \left[ \int_{\mathcal{X} \times \mathcal{X}} \frac{1}{2} \lVert x_1 - x_0 \rVert^2 d\pi(x_0, x_1) -\sigma^2 H(\pi) + \alpha D_{\Psi}(\pi_0\mid q_0) + \beta D_{\Psi}(\pi_1\mid q_1) \right]$

where $\alpha > 0, \beta > 0$ denotes the divergence penalization of the marginal measures.
And $\mathcal{P}\_2(\mathcal{X} \times \mathcal{X})$ is the set of all possible transport plans with normalize condition 

$\int_{\mathcal{X}} d\pi_0 = 1, \quad \int_{\mathcal{X}} d\pi_1 = 1$

We can without loss of generalization insist on the normalization and identity of the initial measure, i.e. 

$\pi^\* = \inf_{\pi_0 = q_0, \pi \in \mathcal{P}\_2(\mathcal{X} \times \mathcal{X})} \left[ \int_{\mathcal{X} \times \mathcal{X}} \frac{1}{2} \lVert x_1 - x_0 \rVert^2 d\pi(x_0, x_1) -\sigma^2 H(\pi) + \beta D_{\Psi}(\pi_1\mid q_1) \right]$

If $\Psi$ is a convex indicator, i.e. $\Psi(1) = 0$ and $\Psi(x) = \infty$ elsewhere. 
Then $D_{\Psi}(\pi_1|q_1) = 0$ if $\pi_1=q_1$ almost surely and $\infty$ otherwise. 
In this case EUOT becomes EOT. 

## EUOT with unnormalized density

We can extend the EUOT problem to unnormalized density space $\mathcal{M}\_2$, without satisfying the normalize condition, to arrive at the Unnormalized Entropy Unbalance Optimal Transport (UEUOT): 

$\pi^\* = \inf_{\pi_0 = q_0, \pi \in \mathcal{M}\_2(\mathcal{X} \times \mathcal{X})} \left[ \int_{\mathcal{X} \times \mathcal{X}} \frac{1}{2} \lVert x_1 - x_0 \rVert^2 d\pi(x_0, x_1) -\sigma^2 H(\pi) + \beta D_{\Psi}(\pi_1\mid q_1) \right]$

We now prove the mass of $\pi_1^\*$ equivalent to the mass of $\pi_0^\*$, i.e. transported mass is conserved. 
A strong duality holds {genevayEntropyregularizedOptimalTransport}, thanks to the Fenchel-Rockafellar theorem {singerFenchelRockafellarTypeDuality1979}:

$\sup_{u, v} \int_{\mathcal{X}} u(x_0)dq_0 - \int_{\mathcal{X}} \Psi^\*(-v(x_1))dq_1 - \epsilon \int_{\mathcal{X} \times \mathcal{X}} e^{\frac{u(x_0) + v(x_1) - c(x_0, x_1)}{\epsilon}} dq_0 dq_1$

where $u$ and $v$ are the potential function of state space $\mathcal{X}$, $c(x_0, x_1)$ is the cost function of transportation, $\epsilon$ is some regularization parameter. 
The first variation with respect to the pair of optimal potential $(u^\*, v^\*)$ is 

$\int_{\mathcal{X}} \delta u u^\*(x_0)dq_0 - \int_{\mathcal{X}} \delta v \Psi^{\*'}(-v^\*(x_1))dq_1 - \int_{\mathcal{X} \times \mathcal{X}} (\delta u + \delta v) e^{\frac{u^\*(x_0) + v^\*(x_1) - c(x_0, x_1)}{\epsilon}} dq_0 dq_1

Reordering the first variation with respect to $\delta v$, we have 

$\Psi^{\*'}(-v^\*(x_1)) = \int e^{\frac{u^\*(x_0) + v^\*(x_1) - c(x_0, x_1)}{\epsilon}} dq_0$

Using the primal-dual relationship \cite{sejourneUnbalancedOptimalTransport2023}

$d\pi^\*(x_0, x_1) = e^{\frac{u^\*(x_0) + v^\*(x_1) - c(x_0, x_1)}{\epsilon}} dq_0dq_1$

We have

$\pi^\*_1(x_1) = \int \pi^\*(x_0, x_1) dx_0 = \left( e^{\frac{u^\*(x_0) + v^\*(x_1) - c(x_0, x_1)}{\epsilon}} dq_0 \right) q_1(x_1) = \Psi^{\*'}(-v^\*(x_1)) q_1(x_1)$

Since the variation can be arbitrary, we let $(\delta u, \delta v) = (\lambda, -\lambda)$, and the last term becomes zero, we have

$\int \lambda dq_0 - \int \lambda \Psi^{\*'}(-v^\*(x_1))dq_1 = \lambda \left(m(q_0) - \int \pi^\*_1(x_1)\right) = 0$

where $m(\cdot)$ is the mass of measure. 
The last equality is due to the fact that of optimal potential $(u^\*, v^\*)$, then all the variants are zero. 
Therefore, we have $\int \pi^\*_1(x_1) = m(q_0)$.
We can always assign $m(q_0) = 1$, and recover the original measure with a constant. 
In this way, $\pi^\* \in \mathcal{P}_2(\mathcal{X} \times \mathcal{X})$, and UEUOT is equivalent to EUOT. 

## Unbalanced SB problem

Within the context, since $\Psi^{'}\_\infty = \infty$, $P_1^\*$ is absolutely continuous with respect to $q_1$.
Therefore, as a mass conserved stochastic mapping between $q_0$ and $P_1^\*$, we can also define a stochastic process $\{Y_t^u\}$

$dY_t^u = u(t, Y_t^u)dt + \sigma dW_t, \quad Y_0^u \sim q_0$

whose Fokker-Planck equation is 

$\partial_t \rho_t + \nabla \cdot (u_t \rho_t) - \frac{1}{2}\sigma^2 \Delta \rho_t = 0, \quad \rho_0 = q_0$

Using the decomposition 

$KL(P^u \mid Q) = D(P_{0, 1}^u \mid Q_{0, 1}) + \int_{\mathcal{X} \times \mathcal{X}} \int_{0}^{1} KL(P_t^u(\cdot \mid x_0, x_1) \mid Q_t(\cdot \mid x_0, x_1)) dt dP_{0, 1}(x_0, x_1)$

where $P_{0, 1}$ is the joint distribution of $q_0$ and $P_1^\*$. 
We have $KL(P^\*|Q) = D(P_{0,1}^\*|Q_{0,1})$. 
Then, the static UEUOT problem Eq.~\ref{eq:UEUOT} is reformulated to a dynamical problem

$\pi^\* = \inf_{\pi_0 = q_0, \pi \in \mathcal{M}\_2(\mathcal{X} \times \mathcal{X})} \left[ \int_{\mathcal{X} \times \mathcal{X}} \frac{1}{2} \lVert x_1 - x_0 \rVert^2 d\pi(x_0, x_1) -\sigma^2 H(\pi) + \beta D_{\Psi}(\pi_1 \mid q_1) \right]$

$\inf_{\pi_0 = q_0, \pi \in \mathcal{P}\_2(\mathcal{X} \times \mathcal{X})} \left[ D(P_{0, 1}^\* \mid Q_{0, 1}) +  \beta D_{\Psi}(\pi_1 \mid q_1)\right]$

$\inf_{\pi_0 = q_0, \pi \in \mathcal{P}\_2(\mathcal{X} \times \mathcal{X})} \left[ KL(P^\*| Q_{0, 1}) +  \beta D_{\Psi}(\pi_1 \mid q_1)\right]$

The above equation implies an unbalanced SB (uSB) problem

$u^\* = \inf_u KL(P^u\mid Q) + \beta D_\Psi(P_1^u|q_1), \quad dQ_t = \sigma dW_t, \quad Q_0 = q_0$

where $u$ induced the path measure $P^u$. 
It can be reformulated in the following expressions using Girsanov's theorem \cite{sarkkaAppliedStochasticDifferential2019}

$u^\* = \inf_u \int_{0}^{1} \int_{\mathcal{X}} \frac{1}{2}\mid|u_t(x)||^2 d\rho_t(x) dt + \beta D_\Psi(\rho_1|q_1)$

s.t.

$\partial_t \rho_t + \nabla \cdot (u_t \rho_t) - \frac{1}{2} \sigma^2 \Delta \rho_t = 0, \quad \rho_0 = q_0$

with marginal conditions $P_0^u = q_0$. 
Similar to EOT, the reciprocal property indicates the marginal-conditioned measure of optimal path $P_t^u$ is a Brownian bridge 

$P_t^\*(\cdot\mid x_0, x_1) = Q_t(\cdot\mid x_0, x_1) = \mathcal{N}(\cdot\mid (1-t)x_0 + tx_1, \sigma^2 t(1-t)I)$

And the solution of uSB problem satisfy 

$KL(P^\*\mid Q) + \beta D_\Psi(P_1^u\mid q_1) = D(P_{0, 1}^\*\mid Q_{0, 1}) + \beta D_\Psi(P_1^u\mid q_1)$

for the optimal path measure, which has the same solution as EUOT by assigning $\pi^\* = P_{0, 1}^\*$. 
Therefore, uSB problem is equivalent to the EUOT problem 

$P_{0, 1}^\* = \pi^\* = \inf_{\pi \in \Pi(q_0, q_1)} \int \frac{1}{2}\mid|x_1 - x_0\mid|^2 d\pi(x_0, x_1) - \sigma^2 H(\pi) + \beta D_\Psi(\pi_1\mid q_1)$

$P_t^\*(\cdot\mid x_0, x_1) = Q_t(\cdot\mid x_0, x_1), \quad (x_0, x_1) \sim P^\*\_{0, 1}$

The optimal path measure is obtained by integral 

$P_t^\*(x) = \int P_t^\*(x|x_0, x_1) dP_{0, 1}^\*$

which is an infinite mixture of Brownian bridges weighted by an EUOT plan. 


