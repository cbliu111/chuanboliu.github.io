---
title: "Stochastic entropy, irreversibility, and neural efficiency"
date: 2022-11-11
categories:
  - blog
tags:
  - theory
  - brain
math: true
---

## Stochastic entropy

The second law of thermodynamics states that the macro-entropy of an isolated object will never decrease. 
If we further divide the object into the system under observation and the larger part served as the reservior environment, we have

$S_{tot} = \Delta S_{sys} + S_{env} \ge 0$

This macro-entropy is purely a statistical effect and further gives the direction of time, which is not sensiable in the microscopic fundamental dynamical equations since they are exactly reversible. 
A good book, E. Fermi, ''Thermodynamics'' (1937). 
In the following we mainly follow the work of Udo Seifert: 
Seifert, U. (2005). "Entropy production along a stochastic trajectory and an integral fluctuation theorem." Phys Rev Lett 95(4): 040602.
For an overdamped Langevin equation 

$\dot{x} = \mu F(x, t) + \sqrt{2D} \xi(t)$

where $D = k_B T \mu $, $\langle \xi(t)\xi(t')\rangle = 2D \delta(t-t')$. 
The corresponding Fokker-Planck equation is 

$\partial_t P(x, t) = -\partial_x (\mu F(x, t) P(x, t)) + D \partial_{xx} P(x, t) = -\partial_x J(x, t) $

We then define the stochastic system entropy as

$S_{sys}(x, t) \equiv -k_B \ln P(x, t)$

where $P(x, t)$ is obtained by solving the Fokker-Plank equation, which means the probability density of finding the system on state $x$ at time $t$. 
We thus see the stochastic system entropy is a state function, as demanded in thermodynamics. 

Given an intial probability distribution of the system, $P(x, t)$ can also be obtained by summing up all the paths that end on state $x$ 
at time $t$. So we see $P(x, t)$ is also a function of the stochastic path. So the stochastic system entropy defined in this form is also a trajectory function. 
But the actual value can not be obtained from a measurement of a single trajectory. 
The path ensemble distribution should be measured in order to obtain $P(x, t)$. 
The path ensemble average can also be instead expressed with

$\langle S_{sys}(x, t) \rangle = -k_B \int \ln P(x, t) p[x(t)]d[x(t)] = -k_B \int \ln P(x, t) P(x, t) dx$

which recovers the Gibbs-Shannon entropy, and the average of system entropy is then the information loss $\left< \Delta S_{sys} \right> = -k_B [H(t) - H(0)]$, 
where $H(t) = -\int p(x, t) \ln p(x, t) dx \ge 0$. 

We now calculate the entropy production rate of the stochastic system entropy,
we should always employ the Stratonovich product whenever encountered in the production between stochastic variables

$\frac{d}{dt} S_{sys}(x, t) = -k_B \left[ \frac{\partial_t P(x, t)}{P(x, t)} + \frac{\partial_x P(x, t)}{P(x, t)} \circ \frac{dx}{dt} \right]$

since $J = \mu F P - D \partial_x P$, substitute in and we have

$\frac{d}{dt} S_{sys}(x, t) = -k_B \left[ \frac{\partial_t P(x, t)}{P(x, t)} + \frac{F(x, t)}{k_B T} \circ \frac{dx}{dt} -\frac{J(x, t)}{DP(x, t)} \circ \frac{dx}{dt}\right]$

From the stochastic first law, $\delta Q(t) = -F(x, t) \circ dx$, then the entropy production rate of the environment is 

$\dot{S}_{env}(t) = - \frac{\dot{Q}(t)}{T} = \frac{F(x, t)}{T} \circ \frac{dx}{dt}$

The total entropy production rate is then

$\dot{S}_{tot}(t) = \dot{S}_{sys}(t) + \dot{S}_{env}(t) = k_B \left[ -\frac{\partial_t P(x, t)}{P(x, t)} +\frac{J(x, t)}{DP(x, t)} \circ \frac{dx}{dt}\right]$

Integrate and we have the entropy production within a time interval 

$S_{tot} (\tau) = \int_0^\tau \dot{S}_{tot}(s)ds = k_B \int_0^\tau \left[ \frac{J(x, t)}{DP(x, t)} \circ dx - \partial_s \log P(x, s) ds \right]$

An important property of the stochastic total entropy is, it is fluctuating and it can be negative. 
We can then estimate the average of the total entropy production rate,

$\langle \dot{S}_{tot}(t) \rangle =  k_B \langle -\frac{\partial_t P(x, t)}{P(x, t)} \rangle + k_B\langle\frac{J(x, t)}{DP(x, t)} \circ \frac{dx}{dt}\rangle$

And the first term vanishes due to conservation of probability

$\langle \frac{\partial_t P(x, t)}{P(x, t)} \langle = \int \frac{\partial_t P(x, t)}{P(x, t)} P(x, t) dx = \partial_t \int P(x, t) dx = \partial_t 1 = 0$

For the second term, we can transform it into Ito formulation by noticing 

$\langle \frac{J(x, t)}{DP(x, t)} \circ \frac{dx}{dt}\rangle = \langle \frac{J(x, t)}{DP(x, t)} \mu F(x, t) dt\rangle  + \langle \frac{J(x, t)}{DP(x, t)} \circ \sqrt{2D} dW \rangle$

We can see for an arbitrary function

$h(x, t) \circ dW = h(x, t) dW + \frac{1}{2} \sqrt{2D}\partial_x h(x, t) dt$

The proof is simple, just expand the product of $h(x, t) \circ dW$ 
at the mid-point of the time step, and dropping all the terms that have higher order than $dt$. 

$\langle \frac{J(x, t)}{DP(x, t)} \circ \sqrt{2D} dW \rangle = \langle \sqrt{\frac{2}{D}} \frac{J(x, t)}{P(x, t)} dW \rangle + \langle \frac{\partial_x J(x, t)}{P(x, t)} dt \rangle - \langle \frac{J(x, t)}{P^2(x, t)} \partial_x P(x, t)dt \rangle$

The first term is then 0 for Wiener process. 
The second term is 

$\langle \frac{\partial_x J(x, t)}{P(x, t)} dt\rangle = \int \frac{\partial_x J(x, t)}{P(x, t)} P(x, t) dx dt = \int \partial_x J(x, t) dx dt = [J(x_f, t) - J(x_0, t)]dt = 0$

since for a fixed region, the probability is conserved within the boundary. 
Therefore, we have the average total entropy production rate as 

$\langle \dot{S}_{tot}(t) \rangle = k_B \langle \frac{J(x, t)}{DP(x, t)} F(x, t) - \frac{J(x, t)}{P^2(x, t)} \partial_x P(x, t)\rangle$

Taken out $\frac{J(x, t)}{DP^2(x, t)}$ and we see the remaining part is just $J(x, t) = \mu F(x, t) P(x, t) - D \partial_x P(x, t)$, we obtain 

$\langle \dot{S}_{tot}(t) \rangle = k_B \langle \frac{J^2(x, t)}{DP^2(x, t)}\rangle  = k_B \int \frac{J^2(x, t)}{DP^2(x, t)} P(x, t) dx = k_B \int \frac{J^2(x, t)}{DP(x, t)} dx \ge 0$

This is the second law of stochastic thermodynamics $\langle \dot{S}_{tot}(t) \rangle \ge 0$

That is, on average, the total entropy production is always non-negative. 
In equilibrium, the probability flux is $J (x, t) = 0$ (can be verified by applying detailed balance condition in a small region, and remember $J(x, t)$
is just the net probability flux into this region), thus $\langle \dot{S}_{tot}(t) \rangle = 0$. 

For discrete system, the master equation 

$\dot{P}\_x(t) = \sum_{y \neq x} \left[ P_y (t)k_{yx}(t)  - P_x (t)k_{xy}(t) \right]$

describes the probability changing rate of the state $x$ at time $t$. 
The transition rate is the transition probability time density from $x \to y$ at time $t$. 
In equilibrium, we have the Boltzmann distribution $P_x(t) = \frac{1}{Z} e^{-E_x/k_B T}$, and detailed balance condition gives

$\frac{k_{xy}}{k_{yx}} = \frac{P_y(t)}{P_x(t)} = e^{-(E_y-E_x)/k_BT}$

For nonequilibrium situation, we see the jump between states are heat driven, that is, the jump between states is coupled with heat dissipation, so we define

$\frac{k_{xy}}{k_{yx}} = e^{-Q_{xy}/k_BT} = e^{S_{xy}^{env}/k_B} = e^{-(E_y(\lambda(t))-E_x(\lambda(t)))/k_BT}e^{-\epsilon_{xy}/k_BT}$

the last equation used the first law of thermodynamics. The above equation is usually called the generalized detailed balance or the local detailed balance. 
The entropy production is 

$dS_{sys}(t) = S_y^{sys} - S_x^{sys} =  -k_B \ln P_y(t) + k_B \ln P_x(t) = k_B \ln \frac{P_x(t)}{P_y(t)}$

Changing of environment entropy during the jump is obtained from the above generalized detailed balance condition $\delta S_{env}(t) = k_B \ln \frac{k_{xy}}{k_{yx}}$.

So the total entropy change is 

$\delta S_{tot} = dS_{sys} + \delta S_{env} = k_B \ln \frac{P_x k_{xy}}{P_y k_{yx}} = k_B \ln \frac{P(s(t)=x, s(t+dt) = y)}{P(s(t)=y, s(t+dt) = x)}$

where $P(s(t)=x, s(t+dt) = y)$ is the joint probability that the system is at state $x$ at time $t$ and then jumps to state $y$ at time $t + dt$, 
it is just the probability of the trajectory $x \to y$. 
And $P(s(t)=y, s(t+dt) = x)$ is just just the probability of the reversed trajectory $y \to x$. 

The environment entropy change between the jumps will be $\delta S_{env}  = 0$ according to the assumption of time scales, so there will be no heat change between jumps. 
The entropy production rate of the system between jumps is then 

$\frac{dS_{sys}}{dt} = -k_B \frac{d\lambda }{dt} \frac{\partial}{\partial \lambda} \ln P_x (\lambda(t)) = \frac{k_B}{P_x(\lambda(t))} \frac{d\lambda}{dt} \frac{\partial P_x(\lambda(t))}{\partial \lambda}$

The average is then

$\langle \frac{dS_{sys}}{dt}\rangle = k_B \sum_x \frac{d\lambda}{dt} \frac{\partial P_x (\lambda(t))}{\partial \lambda} = k_B \frac{d\lambda}{dt} \frac{\partial}{\partial \lambda} \sum_x P_x (\lambda(t)) = 0$

Thus, on average, entropy change of both the environment and the system are all 0 between jumps. Thus entropy change only happens within the jumps. 
Define the net probability current from $x \to y$

$J_{xy}(t) = P_x(t)k_{xy}(t)-P_y(t)k_{yx}(t)$

So net average entropy production rate is just the summation of product of $J_{xy}(t)$ and the total entropy of the jump, we thus have 

$\left<\dot{S}\_{tot}\right> = \frac{k_B}{2} \sum_{xy} J_{xy}(t) \ln \frac{P_xk_{xy}}{P_yk_{yx}}$

$\left<\dot{S}\_{sys}\right> = \frac{k_B}{2} \sum_{xy} J_{xy}(t) \ln \frac{P_x}{P_y}$

$\left<\dot{S}\_{env}\right> = \frac{k_B}{2} \sum_{xy} J_{xy}(t) \ln \frac{k_{xy}}{k_{yx}}$

Denote the forward and backward path distribution density as

$P[x(t)]$: path probability density to observe trajectory $x(t)$  in the forward manipulation protocal $\lambda(t)$

$P[\hat{x}(t)]$: path probability density to observe the time reversed trajectory $\hat{x}(t) = x(t_f -t)$ in the backward manipulation protocol $\hat{\lambda}(t) = \lambda(t_f - t)$

Assuming $P(\hat{x}_0, t_0 )  = P(x_f, t_f)$ that is, the trajectory distribution of the forward paths at $t_f$ is the same as the trajectory 
distribution of the backward paths at their $t_0$. 
So the backward paths are then the paths obtained by reversing the time clock when the forward paths evolved after time $t_f$. We obtain 

$\frac{P[x(t)]}{P[\hat{x}(t)]} = \frac{P(x_0, t_0)}{P(x_f, t_f)} \frac{P[x(t)|x_0]}{P[\hat{x}(t)|x_f]} = e^{-\ln \frac{P(x_f, t_f)}{P(x_0, t_0)}} e^{-Q(x)/k_BT} = e^{S_{tot}[x(t)]/k_B}$

Or in more illustrative form 

$S_{tot}(t) = k_B \ln \frac{P[x(t)]}{P[\hat{x}(t)]}$

The total entropy change is then assigned to the entropy difference between the forward and time reversed backward trajectories. 
In equilibrium, we have obviously $P[x(t)] = P[\hat{x}(t)]$ due to detailed balance condition, which gives $S_{tot}(t) = 0$,  but for nonequilibrium
$S_{tot}(t)$ will fluctuate but with the path ensemble average obeys the second law  $\left<S_{tot}(t)\right> \ge 0$. 


## Neural efficiency and stochastic entropy 

In stochastic thermodynamics, every neural computation (synaptic transmission, action potential) has a cost measured in entropy production.

**Total Entropy Production**: This measures the irreversibility of the neural process. 
If we played a movie of a neuron firing backwards, it would look physically impossible. 
That "time arrow" is the entropy produced.

**Housekeeping Heat**: The energy required just to maintain the resting potential (non-equilibrium steady state).

**Excess Heat**: The extra energy dissipated during the actual computation (firing).

**Ratio of Mutual Information to Thermodynamic Cost:**
Efficiency is now often defined as $E = I/W$, where $I$ is the mutual information (bits transmitted) and $W$ is the thermodynamic work required. 
Recent studies suggest cortical networks maximize this ratio, operating at a "critical point" between order and chaos.

**Sub-kT Computing:**
Some intracellular processes might operate below the $k_B T$ limit by utilizing correlations between fluctuations, 
essentially "harvesting" noise, though this is still debated.







































