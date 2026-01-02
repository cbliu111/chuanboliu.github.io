---
title: "Fluctuation theorem and neural efficiency"
date: 2023-01-20
categories:
  - blog
tags:
  - theory
  - brain
math: true
---

## Fluctuation theorem 

Stochastic thermodynamics describes the statistical features of the stochastic trajectory ensembles. 
We will follow G.E. Crooks: 
Crooks, G. E. (2000). "Path-ensemble averages in systems driven far from equilibrium." Physical Review E 61(3): 2361-2366.
Define the forward trajectory

$[x(t)] = (x_0, x_1, \ldots, x_t)$

and the time-reversed backward trajectory

$[\hat{x}(t)] = (\hat{x}\_0, \hat{x}\_1, \ldots, \hat{x}\_t) = (x_t, x_{t-1}, \ldots, x_0)$

such that the sequence of states visited is a time mirror of the forward trajectory: $\hat{x}\_\tau = x_{t-\tau}$

We then consider the stochastic process of the system between two equilibrium state. 
That is, the initial state $x_0 = \hat{x}_t$ and the final state $x_t=\hat{x}_0$ are all in equilibrium. 

Thus, the state probability distribution according to the Boltzmann distribution is 

$P(x_0, 0) = e^{-\beta (E(x_0, 0) - F_0)}$

$P(\hat{x}\_0, 0) = P(x_t, t) = e^{-\beta (E(x_t, t) - F_t)}$

With free energy $F_\tau$ a deterministic function of time 

$F_\tau = -k_B T \ln \sum_x e^{-\beta E(x, \tau)}$

Thus, the probability density ratio of the forward trajectory with its backward trajectory is 

$\frac{P[x(t)]}{P[\hat{x}(t)]} = \frac{P(x_0, 0)P[x(t)|x_0, 0]}{P(\hat{x}_0, 0)P[\hat{x}(t)|\hat{x}_0, 0]} = e^{\beta(\Delta E - \Delta F)} e^{-\beta Q[x(t)]}$

according to the above equilibrium distribution and the time-scale separation assumption used by the second law of stochastic thermodynamics. 

$Q[x(t)]$ and $\Delta E[x(t)]$ are both functional of the stochastic trajectories, 
and we can apply the first law of the stochastic thermodynamics to obtain the fluctuated work

$W[x(t)] = \Delta E[x(t)] - Q[x(t)]$

$\frac{P[x(t)]}{P[\hat{x}(t)]} = e^{\beta ( W[x(t)] - \Delta F)} = e^{\beta W_{diss}[x(t)]} = e^{S_{tot}[x(t)]/k_B}$

the last equation employs the second law, and $W_{diss}[x(t)]$ is the energy dissipated along this trajectory. 

Tha above equation implies $S_{tot}[x(t)] = k_B \ln \frac{P[x(t)]}{P[\hat{x}(t)]}$

This equation is central in stochastic thermodynamics, since it relates the entropy production with the irreversibility of the trajectory, i.e. the asymmetry trajecotry ensemble distribution quantifies the entropy production. 
We then see the relative probability weight relation between the forward and backward trajectories depends on the entropy production, or on the amount of energy dissipated. 
We can use this relationship to calculate the average value of some properties of the system given the forward trajectory ensemble and the backward trajectory ensemble. 
For doing that, we define a functional along the forward or the backward trajectory as 

$\Omega[x(t)]: [x(t)] \to \mathbb{R}$, $\Omega[\hat{x}(t)]: [\hat{x}(t)] \to \mathbb{R}$

And we further demand $\Omega$ is not changed during the time-reverse transformation, $\Omega[x(t)] = \Omega[\hat{x}(t)]$, The forward average is then 

$\langle \Omega[x(t)]\rangle_F = \int \Omega[x(t)] P[x(t)] d[x(t)] = \int \Omega[x(t)] P[\hat{x}(t)]e^{\beta W_{diss}[x(t)]} d[x(t)]$

And the dissipated energy of the reversed process is 

$W_{diss}[\hat{x}(t)] = k_B T \ln \frac{P[\hat{x}(t)]}{P[x(t)]} = - k_B T \ln \frac{P[\hat{\hat{x}}(t)]}{P[\hat{x}(t)]}$

which demands the calculation of $P[\hat{\hat{x}}(t)]$
 as a double-reverse process. However, it is not necessarily equal to 
$P[x(t)]$ , that is, the backward-of-the-backward trajectory probability is equal to the forward trajectory probability. This requires the backward trajectory given 
$P(x_t, t)$
 will reproduce the initial 
$P(x_0, 0)$
 , otherwise given different initial distribution but follow the same stochastic dynamical equation will never recover 
$P(x_t, t)$
 . It is not always the case, since the backward trajectory will depends on the backward manipulation protocol 
$\hat{\lambda}(t)$
 . But for a steady-state (not necessarily in equilibrium), since the state distribution is stationary along time, i.e. 
$P(x_t, t) = P(x_0, 0)$
 , the backward trajectory always recover the initial distribution of the forward trajectory, thus we always have 
$P[\hat{\hat{x}}(x)] = P[x(t)]$
 . And for the above setting, where initial and final state are all equilibrium, surely they have the same Boltzmann distribution. 
In either way, we have the involution of the dissipated energy 

$W_{diss}[\hat{x}(t)] = -W_{diss}[x(t)]$

and we notice there will always have a one-one correspondence between the forward and backward trajectory, thus 
$d[x(t)] = d[\hat{x}(t)]$
 , so 
 
$\langle \Omega[x(t)]\rangle_F = \int \Omega[\hat{x}(t)] P[\hat{x}(t)]e^{-\beta W_{diss}[\hat{x}(t)]} d[\hat{x}(t)] = \langle e^{-\beta W_{diss}[\hat{x}(t)]} \Omega[\hat{x}(t)]\rangle_R$

Or on the other way around, 

$\langle e^{-\beta W_{diss}[x(t)]} \Omega[x(t)]\rangle_F = \langle \Omega[\hat{x}(t)]\rangle_R$

The above equation is applicable to any time-reverse even trajectory functional. 
Now we assign $\Omega[x(t)] = 1$, then we automatically have $\Omega[\hat{x}(t)] = 1$
We then have 

$\langle e^{-\beta W_{diss}[x(t)]}\rangle_F = \langle e^{-\beta (W[x(t)]- \Delta F)}\rangle_F = \langle1\rangle_R = 1$

Thus we have obtained the famous Jarzynski equation

$\langle e^{-\beta W[x(t)]}\rangle_F = e^{-\beta \Delta F}$

We can then assign $\Omega[x(t)] = \delta( W[x(t)] - W)$, therefore $\Omega[x(t)] = \Omega[\hat{x}(t)]$. 
Since for any trajectory, the work done on it is opposite for its time-reverse trajectory $W[x(t)] = -W[\hat{x}(t)]$
hence the value is the same for the forward and the backward trajectory. 
The fluctuation theorem gives 

$\angle\delta (W[x(t)]-W) e^{-\beta W_{diss}[x(t)]}\rangle_F = \langle \delta (W[\hat{x}(t)]+W)\rangle_R$

Since $W_{diss}[x(t)] = W[x(t)] - \Delta F$, we obtain 

$e^{\beta \Delta F} \langle \delta(W[x(t)]-W)e^{-\beta W[x(t)]}\rangle_F = \langle\delta(W[\hat{x}(t)]+W)\rangle_R$

The average of Dirac $\delta$-function gives the weighted probability density sum of the paths where $\delta(\cdot)$ is not zero, thus we have 

$e^{\beta \Delta F} e^{-\beta W} P_F(W) = P_R(-W)$

rearrange and notice the relationship between dissipated energy and the total entropy production we have 

$\frac{P_F(W)}{P_R(-W)} = e^{\beta (W[x(t)]-\Delta F)} = e^{\beta W_{diss}[x(t)]} = e^{S_{tot}[x(t)]/k_B}$

We can also derive many fluctuation relations with respect to various quantities. 
Since $S_{tot}[x(t)] = k_B \ln \frac{P[x(t)]}{P[\hat{x}(t)]}$, We immediately obtained the integral fluctuation relation

$\langle e^{-S_{tot}/k_B}\rangle_F = \int \frac{P[\hat{x}(t)]}{P[x(t)]} P[x(t)]d[x(t)] = \int P[\hat{x}(t)]d[\hat{x}(t)] = 1$

From this equation we can verify the second law easily, since Jensen inequality entails 

$\ln \langle e^{-x}\rangle \ge \ln e^{-\langle x \rangle} = -\langle x \rangle$

 we have 

$\ln \langle e^{-S_{tot}[x(t)]/k_B }\rangle_F = \ln 1 = 0 \ge - \langle S_{tot}[x(t)]/k_B\rangle_F$

so that $\langle S_{tot}[x(t)]\rangle_F \ge 0$. 

We can also derive a similar fluctuation relation analogy to the Crooks relation, but we shall again 
assume that the entropy production is an involution (i.e. odd, or sign changed during time-reverse transformation), that is

$S_{tot}[x(t)] = -S_{tot}[\hat{x}(t)]$

Thus given an arbitrary functional of the trajectory $f(\cdot)$, we have 

$\langle f(S_{tot}[x(t)]) e^{-S_{tot}[x(t)]/k_B}\rangle_F = \int f(S_{tot}[x(t)] )e^{-S_{tot}[x(t)]/k_B} P[x(t)] d[x(t)] \\ = \int f(-S_{tot}[\hat{x}(t)] )P[\hat{x}(t)] d[\hat{x}(t)] = \langle -f(S_{tot}[\hat{x}(t)])\rangle_R$

We assign 

$f(S_{tot}[x(t)]) = \delta (S_{tot}[x(t)] -s ) = \delta (S_{tot}[\hat{x}(t)] +s )$

Thus we have

$\langle\delta(S_{tot}[x(t)]-s) e^{-S_{tot}[x(t)]/k_B}\rangle_F = \langle\delta(S_{tot}[\hat{x}(t)]+s)\rangle_R$

which gives

$\frac{P_F(s)}{P_R(-s)} = e^{S_{tot}[x(t)]/k_B}$

This is called the detailed fluctuation relation. 


## Neural efficiency and fluctuation theorem 

These theorems connect non-equilibrium work to equilibrium free energy differences. They allow researchers to estimate the energy landscape of ion channels opening and closing. They reveal that biology uses thermal noise to assist processes rather than just fighting against it (e.g., Brownian ratchets), which improves efficiency. 

However, cellular components (ion channels, synaptic vesicles, enzymes) are microscopic. At this scale, thermal noise is violent. Sometimes, random thermal energy actually kicks a system "backwards" against the flow of entropy, momentarily violating the Second Law of Thermodynamics.

Fluctuation Theorems quantify these rare events. Here is how they redefine our understanding of Neural Efficiency.

### The Cost of "Thinking" vs. "Living"

A neuron is not a closed system like a piston; it is an open system in a Non-Equilibrium Steady State (NESS). It constantly burns energy just to stay alive (pumping ions), even when not firing.

The Hatano-Sasa Equality is a specific fluctuation theorem for these steady states. It allows physicists to split the brain’s energy bill into two distinct parts:

**Housekeeping Heat ($Q_{hk}$):** The energy burned to maintain the resting potential. This is the "cost of living."

**Excess Heat ($Q_{ex}$)**: The energy burned specifically during a transition (a computation/spike). This is the "cost of thinking."

Neural efficiency is defined by minimizing $$Q_{ex}$ (excess heat) without destabilizing the steady state $Q_{hk}$.

**Inefficient Neuron:** A transition from State A to State B is "rough," generating massive friction and excess heat.

**Efficient Neuron:** The transition follows a "geodesic" path in thermodynamic space. 
The ion channels open in a specific sequence that minimizes the entropy burst. 
Evolution has likely tuned ion channel kinetics (opening speeds) to minimize this Hatano-Sasa excess heat.

| Classical View | Stochastic/Fluctuation View |  
| :--- | :--- |  
| Efficiency = Output / Input Energy | Efficiency = Info gained / Entropy produced |  
| Noise is a nuisance to be overpowered. | Noise is a resource to be rectified. |  
| Cost is determined by mechanics. | Cost is determined by **irreversibility** (the ratio of forward/backward probabilities). |  
| **Goal:** Minimize Heat. | **Goal:** Operate near the **Landauer limit** where $\Delta Q \approx k_B T \ln 2$. |













