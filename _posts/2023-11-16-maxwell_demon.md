---
title: "Maxwell's demon and dissipative information"
date: 2023-11-16
categories:
  - blog
tags:
  - theory
  - field theory
math: true
---

We will follow 
Sagawa, T. and M. Ueda (2010). "Generalized Jarzynski equality under nonequilibrium feedback control." Phys Rev Lett 104(9): 090602.
Qian, Z. and W. Jin (2021). "New fluctuation theorems on Maxwell’s demon." Sci Adv 7 : eabf1807
A Maxwell's demon is an object that perform a programmable operation policy on a stochastic dynamical system based on the instanteneous measurement result. 
At time $t_m$, the system has a state distribution $P(x_m)$ , when performing a non-perfect measurement, the output is distributed as $P(y_m \mid x_m)$, thus the state of the demon is distributed as $P(y_m) = \int dx_m P(y_m \mid x_m) P(x_m)$. 

The degree of correlation between the measurement output and the state of the system is quantified by the mutual information

$\left<I_m\right> \equiv \int dx_m dy_m P(y_m \mid x_m)P(x_m) \ln \frac{P(y_m \mid x_m)}{P(y_m)}$

Suppose the feed back control $\lambda(t; y)$ performed by the demon is a bijective deterministic protocol based on the measurement, there will be a time-reversed control $\lambda^\dagger (t; y^\dagger)$ corresponds to the time-reversed trajectory $x^\dagger(t) \equiv x^*(\tau -t)$ where $y^\dagger \equiv y^*(\tau-t)$  is also time-reversed. 

Now we consider the trajectory ensemble distribution of the forward trajectory $P[x(t); \lambda(t; y(t))]$ and backward trajectory $P[x^\dagger (t); \lambda^\dagger (t; y^\dagger(t)]$ , with normalization $\int d[x(t)] P[x(t); \lambda(t; y(t))] = 1$, $\int d[x^\dagger(t)] P[x^\dagger(t); \lambda^\dagger(t; y^\dagger(t))] = 1$, where we have $d[x(t)] = d[x^\dagger(t)]$. 

We will assume local detailed balance since the system is connected with a large thermal bath, which means 

$e^{\sigma_X} = \frac{P[x(t); \lambda(t; y(t))]}{P[x^\dagger(t); \lambda^\dagger(t; y^\dagger(t))]}$

for situations that $y(t)$ and $y^\dagger(t)$ does not dependent on the measurement results. 

If there is a feed back control, the system state $x(t)$ and $x^\dagger(t)$ are actually correlated with the measurement output, thus the joint trajectory distribution should be considered instead of the marginal trajectory distribution 

$P[x(t), y(t)] = P[y(t)|x(t)]P[x(t); \lambda(t, y(t)]$

We then redefine the trajectory mutual information as $I \equiv \ln \frac{P[y(t)|x(t)]}{P[y(t)]}$ Then 

$\left<e^{-\sigma_X-I}\right> = \int d[y(t)]d[x(t)] P[y(t), x(t)] \frac{P[x^\dagger(t); \lambda^\dagger(t; y^\dagger(t))]}{P[x(t); \lambda(t; y(t))]} \frac{P[y(t)]}{P[y(t)|x(t)]} \\ = \int d[y(t)]d[x(t)] P[x^\dagger(t); \lambda^\dagger(t; y^\dagger(t))] P[y(t)] \\ = \int d[y(t)]d[x^\dagger(t)] P[x^\dagger(t); \lambda^\dagger(t; y^\dagger(t))] P[y(t)] =1$ 

which is the so called generalized Jarzynski equation

$\left<e^{-\beta(W-\Delta F) -I}\right> = 1$

by counting the mutual information of the feed back control.
Using Jensen inequality we have $\left<W\right> \ge \Delta F - k_BT\left<I\right>$

This is the lower bound obtained by Sagawa and Ueda. 
However, since the system state is under control, there is no reason to use the original trajectory ensemble distribution to calculate the entropy production. What should be used is the conditional trajectory ensemble distribution, and define the conditional entropy production as 

$e^{\sigma_{X|Y}} = \frac{P[x(t)|y(t); \lambda(t, y(t)]}{P[x^\dagger(t)|y^\dagger(t); \lambda^\dagger(t, y^\dagger(t)]}$

And introduce the information dissipative term

$\sigma_I = I-I^\dagger = \ln \frac{P[x(t)|y(t); \lambda(t, y(t)]}{P[x(t); \lambda(t, y(t)]} - \ln \frac{P[x^\dagger(t)|y^\dagger(t); \lambda^\dagger(t, y^\dagger(t)]}{P[x^\dagger(t); \lambda^\dagger(t, y^\dagger(t)]} \\ = \ln \left\\{\frac{P[x(t)|y(t); \lambda(t, y(t)]}{P[x^\dagger(t) \mid y^\dagger(t); \lambda^\dagger(t, y^\dagger(t)]}\frac{P[x^\dagger(t); \lambda^\dagger(t, y^\dagger(t)]}{P[x(t); \lambda(t, y(t)]}\right\\}$

which describe the irreversibility of information transfer from the demon to the system. 
By assuming fixed demon state, that is, $y^\dagger(t) = y(\tau-t)$, we have $P[y^\dagger(t)] = P[y(t)]$, therefore $\sigma_I =\ln \frac{P[y(t)|x(t)]}{P[y(t)|x^\dagger(t)]}$ , together with  $\sigma_{X|Y} = \ln \frac{P[x(t)|y(t); \lambda(t, y(t)]}{P[x^\dagger(t)|y(t); \lambda(t, y(t)]}$, $\sigma_{X} = \ln \frac{P[x(t)]}{P[x^\dagger(t)]}$ satisfying $\sigma_{X|Y} = \sigma_X + \sigma_{I}$. 

We obtain the generalized Jazynski equations for dissipative information 

$\left<e^{-\sigma_I}\right> =\int d[x(t)] d[y(t)]P[y(t)|x(t)] P[x(t); \lambda(t, y(t))]\frac{P[y(t)|x^\dagger(t)]}{P[y(t)|x(t)]} \\ = \int d[x(t)] d[y(t)] P[x(t); \lambda(t, y(t))] P[y(t)|x^\dagger(t)] = 1$

$\left<e^{-\sigma_{X|Y}}\right> = \int d[x(t)] d[y(t)] P[y(t)]P[x(t)|y(t); \lambda(t, y(t)] \frac{P[x^\dagger(t)|y^\dagger(t), \lambda(t, y^\dagger(t)]}{P[x(t)|y(t), \lambda(t, y(t)]} \\ = \int d[x(t)] d[y(t)]P[y(t)]P[x^\dagger(t)|y^\dagger(t), \lambda(t, y^\dagger(t)] \\ = \int d[x(t)] d[y(t)]P[x^\dagger(t), y(t)] = 1$

$\left<e^{-\sigma_{X}}\right> = \int d[x(t)] P[x(t); \lambda(t, y(t)] \frac{P[x^\dagger(t);  \lambda(t, y^\dagger(t)]}{P[x(t); \lambda(t, y(t)]} \\ = \int d[x^\dagger(t)] P[x^\dagger(t);  \lambda(t, y^\dagger(t)] = 1$

with different normalization protocols.











