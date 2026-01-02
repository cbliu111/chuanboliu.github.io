---
title: "Probability for negative entropy production"
date: 2023-09-10
categories:
  - blog
tags:
  - theory
  - field theory
math: true
---

From Crooks fluctuation relation we have 

$\ln\left(\frac{P_F(W)}{P_R(-W)}\right) = \frac{1}{k_B T} (W - \Delta F)$

Thus if the system is at equilibrium then $P_F(W) = P_R(-W)$ as demanded by the detailed balance condition.
So that $W = \Delta F$ , and since at equilibrium, $\Delta F$ does not fluctuates, we then can write $P(W) = \delta(W-\Delta F)$ for equilibrium work distribution. 

While if the system is not at equilibrium, we will have a more broad distribution of work, and the average is larger than the free energy change. This can be shown by applying Jensen inequality to Jarzynski relation 

$\Delta F = -k_B T \ln \left<e^{-\frac{W}{k_B T}}\right> \le -k_B T \ln e^{-\frac{\left<W\right>}{k_B T}} = \left<W\right>$

Such that entropy production will always be positive as demanded by the second law of stochastic thermodynamics. 

$\left<W\right> - \Delta F = TS_{tot} \ge0$

We now calculate the probability that the entropy production is negative along some trajectories, that is, the probability that $W-\Delta F \le -\eta$, where $\eta$ is a positive number which describe the distance between $W$ and $\Delta F$, or how negative is the entropy production since $S_{tot} = -\frac{\eta}{k_BT}$

The probability is the cumulative of the probability density

$Pr(W-\Delta F \le -\eta) = \int_{-\infty}^{\Delta F - \eta} dWP(W)$

Notice here the integral is not a trajectory integral, and $W$  is just a number. 
Since $W-(\Delta F  -\eta) \le 0$, we have $e^{-\frac{1}{k_BT}(W-(\Delta F  -\eta))} \ge 1$. Therefore, 

$Pr(W-\Delta F \le -\eta) \le \int_{-\infty}^{\Delta F - \eta} dWe^{-\frac{1}{k_BT}(W-(\Delta F  -\eta))} P(W) \\ =  e^{\frac{1}{k_BT}(\Delta F  -\eta)}\int_{-\infty}^{\Delta F - \eta} dWe^{-\frac{1}{k_BT}W} P(W) \\ \le e^{\frac{1}{k_BT}(\Delta F  -\eta)}\int_{-\infty}^{\infty} dWe^{-\frac{1}{k_BT}W} P(W) \\ = e^{\frac{1}{k_BT}(\Delta F  -\eta)} \left<e^{-\frac{1}{k_BT}W}\right> = e^{\frac{1}{k_BT}(\Delta F  -\eta)} e^{-\frac{1}{k_BT}\Delta F} = e^{-\frac{1}{k_BT}\eta}$

In short, the probability of having negative entropy production trajectory is exponentially unlikely with respect to the distance from the free energy change. 















