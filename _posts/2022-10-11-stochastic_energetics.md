---
title: "Stochastic energetics and neural efficiency"
date: 2022-10-11
categories:
  - blog
tags:
  - theory
  - brain
math: true
---

## Stochastic energetics

Depending on the size and time scales we can divide the description of (classical) dynamical law into three levels. The finnest is the microscopic level, where events happen in femto- or pico-second, and is usually within atomic scale. This description contains all degrees of freedom of the system, and the evolution is deterministic by conservation of information. The most coarse-grain is the thermodynamic formalism with thermodynamic variables. The divergence of different dynamic laws are averaged out to give well defined behavior of the thermodynamic variables. The intermediate level is what so called stochastic dynamics like the Langevin equation that adopts a probabilistic perspective to the dynamics of system under concern.
Consider a Brownian particle under time-related potential and an external force, we have 

$m \frac{dv}{dt} = -\gamma v - \frac{\partial U(x, t)}{\partial x} + f(x, t) + \xi(t)$

$\langle \xi(t)\rangle = 0$

$\langle \xi(t) \xi(t') \rangle = 2k_B T \gamma \delta (t - t')$

For overdamped limit, that is, $\Delta t \gg m / \gamma$ for mass is small or the friction coefficient is large, we have $\frac{m/\gamma}{dt}dv \to 0$.
Therefore, 

$\frac{\partial U (x, t)}{\partial x} + f(x, t) = -\gamma \frac{dx}{dt} + \xi(t)$

The l.h.s. are forces contributed by the manipulation of poential and the dragging of external source, and the r.h.s. are forces contributed by the friction of the fluid molecules and noise due to collisions by the fluid molecules. It is thus a balance of the external forces with the batch forces. 
The heat that bath transformed to the particle along a trajectory is then a stochastic integral of the production of the batch forces with the displacement

$Q[x(t)] = \int_0^\tau \left(-\gamma \frac{dx}{dt} + \xi(s)\right) \circ dx(s) \\ = \int_0^\tau \left(\frac{\partial U(x, t)}{\partial x} - f(x, s) \right) \circ dx(s)$

And differential form 

$\delta Q(t) = \frac{\partial U(x, t)}{\partial x} \circ dx(t) - f(x, t)  \circ dx(t)$

Here we are using the Stratonovich integral because the Stratonovich differential formula follows the usual rules of calculus, which is essential for estabilishing the balance of energy. 
Since a trajectory of stochastic process can be viewed as a function, so $Q[x(t)]$  is actually a functional along the trajectory $[x(t)]$. 
$Q[x(t)]$ is also a stochastic process that coupled with $[x(t)]$. 

We know from thermodynamics heat is not a state function but depends on the actual trajectory. This is consistent with the above picture. 
Next we should calculate the work along the same trajectory. For work, it should be cautious about the difference of contributions from external forces and bath. e.g. if we systematically change the potential follow a procotol
$\lambda(t)$ while keeping the system state unchanged, there will be work exerting on the particle $\frac{\partial U(x, \lambda(t))}{\partial x} d\lambda$
; if system state is changed without external forces and change of potential, then it is the noise driven event caused by influx of bath heat; if there are displacement causing by the external force, then there will also be work
 $f(x, t) \circ dx(t)$. 

 Taken together, we have the work along a trajectory 

 $W[x(t)] = \int_0^\tau \left( \frac{\partial U(x, \lambda(t))}{\partial \lambda} \frac{d\lambda}{dt} dt + f(x, t) \circ dx(t) \right)$

And differential form $\delta W(t) = \frac{\partial U(x, \lambda(t))}{\partial \lambda} \frac{d\lambda}{dt} dt + f(x, t) \circ dx(t)$

We then sum the heat and work, and since Stratonovich follow the ordinary calculus rules we have 

$\delta W(t) + \delta Q(t) = \frac{\partial U(x, \lambda(t))}{\partial \lambda} d\lambda + \frac{\partial U(x, \lambda(t))}{\partial x} \circ dx(t) = dU(x, \lambda(t))$

Thus, we see the reason of chosing Stratonovich formula. This conservation of energy is valid for any trajectories that satisfied the Langevin equation. 
We can also verify this with Ito formulation, but less intuitive and physical motivated. For doing that, first we prove a relation between Ito and Stratonovich 

$F(x, t) \circ dx = F(x, t) dx + \frac{1}{2} g^2(x, t) \frac{\partial F(x, t)}{\partial x} dt$

The proof is straightforward by expanding 

$F\left(\frac{x_{n+1}+x_n}{2}, t_n\right) = F\left(x_n + \frac{1}{2}\Delta x_n, t_n\right) \\ = F(x_n, t_n) + \frac{1}{2}\Delta x_n \frac{\partial F(x_n, t_n)}{\partial x} + \frac{1}{2}\left(\frac{1}{2}\Delta x_n\right)^2 \frac{\partial^2 F(x_n, t_n)}{\partial x^2}$
By dropping every term higher than $dt$, we obtain 

$F\left(\frac{x_{n+1}+x_n}{2}, t_n\right) \Delta x_n  = F(x_n, t_n) \Delta x_n + \frac{1}{2}(\Delta x_n)^2 \frac{\partial F(x_n, t_n)}{\partial x} \\ = F(x_n, t_n) \Delta x_n + \frac{1}{2}g^2 \frac{\partial F(x_n, t_n)}{\partial x} \Delta t_n$

Thus prove the above relation. 
We can then show

$\delta Q(t) = \frac{\partial U(x, t)}{\partial x} dx(t) - f(x, t)  dx(t) + \frac{1}{2} g^2(x, t) \frac{\partial^2 U(x, t)}{\partial x^2} dt - \frac{1}{2} g^2(x, t) \frac{\partial f(x, t)}{\partial x} dt$

$\delta W(t) = \frac{\partial U(x, \lambda(t))}{\partial \lambda} \frac{d\lambda}{dt} dt + f(x, t) dx(t) + \frac{1}{2} g^2(x, t) \frac{\partial f(x, t)}{\partial x} dt$

$\delta Q(t) + \delta W(t) = \frac{\partial U(x, t)}{\partial x} dx(t) + \frac{1}{2} g^2(x, t) \frac{\partial^2 U(x, t)}{\partial x^2} dt + \frac{\partial U(x, \lambda(t))}{\partial \lambda} d\lambda = dU(x, \lambda(t))$

following the Ito formula.

For discrete Markov jump process, we have various energies that associated with each state $E_{x_n}$, the work done by the external forces are then the sum of the changing of energy due to change of state energy level without jumping and the external forces 

$W(\tau) = \sum_{n=0}^N \int_{t_n}^{t_{n+1}} \frac{d E_{x_n} (t) }{dt} dt + \sum_{n=0}^N \epsilon_{x_n} dx_n$

 where $N$ is the total number of jumps, and heat is given by

 $Q(\tau) = \sum_{n=0}^N \left[\left(E_{x_{n+1}}(t_{n+1}) - E_{x_n}(t_{n+1})\right) - \epsilon_{x_n} x_n\right]$

We see again the conservation of energy as demanded 

$W(\tau ) + Q(\tau) = E_{x_f} (\tau) - E_{x_0} (0)$

To summary, the definition of the heat and energy along a trajectory that described by a Langevin equation satisfied an energy conservation equation. It is usually called the first law of stochastic thermodynamics. 

## Neural efficiency from the perspective of stochastic enegetics

From the stochastic energetic perspective, we can view the brain as a deterministic machine to viewing it as a noisy, heat-dissipating system operating far from equilibrium.
The Core problem is: Information vs. Heat
Classical thermodynamics deals with macroscopic averages, but neurons operate at the mesoscopic scale where thermal fluctuations (noise) are significant.

**The Landauer Limit**: Rolf Landauer showed that erasing 1 bit of information (a necessary step in processing) releases a minimum amount of heat ($k_B T \ln 2$)

**The Brain's Reality**: The brain operates remarkably close to this physical limit compared to modern computers, 
yet it still dissipates significantly more heat than the theoretical minimum. 
Stochastic thermodynamics can help to quantify this "inefficiency cost" of reliability.

### Energy costs of brain

**The Cost of "Sharpness"**: Sharp action potentials require fast sodium entry and potassium exit. 
To make the timing precise (sharp), ion channels must operate rapidly and irreversibly, dissipating high heat.

**The Cost of Counteracting Noise:** Because neurons are small, random thermal motion of ions can trigger false spikes. 
The brain maintains high metabolic barriers to prevent these "accidental" fires.

**Sensory Adaptation:** Stochastic thermodynamics shows that sensory neurons (like in the retina) adjust their energy consumption based on information flow. When visual information is predictable, they lower their dissipation; when it is surprising, they spend more energy to capture the new data.





















