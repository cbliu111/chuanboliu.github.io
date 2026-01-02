---
title: "Stochastic path integral"
date: 2023-03-14
categories:
  - blog
tags:
  - theory
  - field theory
math: true
---

We follow 
Wio, H. S. (2013). "Path Integrals For Stochastic Processes An Introduction."
Seifert, U. (2008). "Stochastic thermodynamics." 39th IFF Spring School, Institut of Solid State Research, Research Centre Julich
Consider a Wiener process $\dot{W}(t) = \xi(t)$, where $\left<\xi(t)\xi(t')\right> = 2D \delta (t - t')$. 

An observable on the stochastic path can be averaged by summation of all trajectories in the path ensemble. 

$\left<A[W]\right> = \int dW_1 dW_2 \ldots dW_N A[W] \left<\delta(W_1 - \hat{W}_1)\delta(W_2 - \hat{W}_2)\ldots\delta(W_N - \hat{W}_N)\right>$

where $N$ is the total number of trajectory partition in the sense that $N \to \infty$, so that in a finite time interval the time of step 
$\Delta t \to 0$ while the total time remain constant $N \Delta t = \tau$. The probability is obtained using the average of $\delta$-function which select the desired path along the trajectory partitions. 

This trajectory partition leads to the discrete form of the stochastic differential equation $W_i - W_{i-1} = \Delta t \xi_{i-1} $
We can rewrite this equation by noting the selected trajectory is just the solution of the Wiener process

$\left<A[W]\right> = \int dW_1 dW_2 \ldots dW_N A[W] \left<\prod_{i=1}^N \delta(W_i - W_{i-1} - \Delta t \xi_{i-1} )\right>$
We can approach this integral through Fourier transformation

$\delta(W_i - W_{i-1} - \Delta t \xi_{i-1} ) = \frac{1}{2\pi}\int dy\ e^{iy(W_i - W_{i-1} - \Delta t \xi_{i-1})}$

And multiplication of uncorrelated variables can be converted into a multiple integration

$\prod_{i=1}^N \delta(W_i - W_{i-1} - \Delta t \xi_{i-1} ) = \left(\frac{1}{2\pi}\right)^N \int \left(\prod_{i=1}^N dy_i\right) \ e^{i \sum_{i=1}^N y_i (W_i - W_{i-1} - \Delta t \xi_{i-1})}$

denote $d[W] = \prod_{i=1}^N dW_i$ and $d[y] = \prod_{i=1}^N dy_i$, we obtain 

$\left<A[W]\right> = \left(\frac{1}{2\pi}\right)^N \int d[W]d[y] A[W] \left< \ e^{i \sum_{i=1}^N y_i (W_i - W_{i-1} - \Delta t \xi_{i-1})} \right>$

note $e^{i \sum_{i=1}^N y_i (W_i - W_{i-1})}$ is not fluctuate and can be taken out of the average integral, and we also know from the property of Gaussian distribution 

$e^{-i \Delta t \sum_{i=1}^N y_i \xi_{i-1}} = e^{-\frac{1}{2} (\Delta t)^2 \sum_{i=1}^N \sum_{j=1}^N y_i y_j \left<\xi_{i-1} \xi_{j-1}\right>} $

and since $\left<\xi_{i-1} \xi_{j-1}\right> = \frac{2D}{\Delta t} \delta_{i,j}$ which approaches a $\delta$-function as $\Delta t \to 0$. We obtain 

$e^{-i \Delta t \sum_{i=1}^N y_i \xi_{i-1}} = e^{-D\Delta t \sum_{i=1}^N y_i^2}$

The average of the observable becomes

$\left<A[W]\right> = \left(\frac{1}{2\pi}\right)^N \int d[W]d[y] A[W] \ e^{i \sum_{i=1}^N [y_i (W_i - W_{i-1}) - D\Delta t y_i^2]} $

We can integrate $y$ out by noticing the integral on the exponential can be turned into an Gaussian integral

$iy_i (W_i - W_{i-1}) - D\Delta t y_i^2 = -D\Delta t \left(y_i^2 - \frac{i y_i (W_i - W_{i-1})}{D \Delta t}\right) \\ = -D\Delta t \left(y_i^2 - \frac{i y_i (W_i - W_{i-1})}{D \Delta t} + \left( \frac{i (W_i - W_{i-1})}{2D \Delta t}\right)^2\right) - \frac{(W_i - W_{i-1})^2}{4D \Delta t} \\ = -D\Delta t \left(y_i - \frac{i (W_i - W_{i-1})}{2D \Delta t}\right)^2 - \frac{(W_i - W_{i-1})^2}{4D \Delta t}$

Since $\int_{-\infty}^\infty e^{-az^2} dz = \sqrt{\frac{\pi}{a}}$, we obtain 

$\left<A[W]\right> = \left(\frac{1}{2\pi}\right)^N \left(\frac{\pi}{D \Delta t}\right)^{N/2} \ \int d[W] A[W] \prod_{i=1}^N e^{-\frac{1}{4D\Delta t}(W_i - W_{i-1})^2} \\ = \left(\frac{1}{4\pi D \Delta t}\right)^{N/2} \ \int d[W] A[W] \prod_{i=1}^N e^{-\frac{1}{4D\Delta t}(W_i - W_{i-1})^2}\\ = \int d[W] A[W] p[W]$

We thus see the weight of a particular trajectory is

$p[W] = \prod_{i=1}^N \frac{1}{\sqrt{4\pi D \Delta t}}  e^{-\frac{1}{4D\Delta t}(W_i - W_{i-1})^2}$

One step weight is 

$\frac{1}{\sqrt{4\pi D \Delta t}}  e^{-\frac{1}{4D\Delta t}(W_i - W_{i-1})^2}$

In continuum limit, it is 

$p[W] = \int d[W] e^{-\frac{1}{4D} \int_0^\tau dt \left(\frac{dW}{dt}\right)^2}$

where we have redefined $d[W] = \prod_{i=1}^N \frac{dW_i}{\sqrt{4\pi D \Delta t}}$

The trajectory distribution of $\xi(t)$ is a transform of the trajectory distribution of $W(t)$, notice that at every time step we have $W_i - W_{i-1} =\Delta t \xi_{i-1} $

We then obtain 

$p[\xi] = \det \left(\frac{\partial W_i}{\partial \xi_j}\right) p[W] = \prod_{i=1}^N \left(\Delta t\  \frac{1}{\sqrt{4\pi D \Delta t}}  e^{-\frac{1}{4D\Delta t}(W_i - W_{i-1})^2}\right) = \prod_{i=1}^N \left( \sqrt{\frac{ \Delta t}{4\pi D}}  e^{-\frac{\Delta t}{4D}\xi_i^2}\right)$

One step weight is $\sqrt{\frac{ \Delta t}{4\pi D}}  e^{-\frac{\Delta t}{4D}\xi_i^2}$. We then turn into a general Langevin equation with the form 

$\dot{x} = \mu F(x, \lambda) + \xi(t)$, where $\lambda = \lambda(t)$ is the manipulation protocol. 

Partition the trajectory follow Stratonovich we have 

$\frac{x_i - x_{i-1}}{\Delta t} = \frac{\mu}{2} [F(x_i, \lambda_i) + F(x_{i-1}, \lambda_{i-1})] + \xi_i$

The path ensemble distribution of this Langevin equation is nothing but a transformation of the Wiener path probability distribution, we thus need to calculate the Jacobi matrix 

$\frac{\partial \xi_i}{\partial x_j} = \left( \begin{array}{1} \frac{1}{\Delta t} - \frac{\mu}{2}\frac{\partial F(x_1, \lambda_1)}{\partial x_1} & 0 &  0 & 0 & \ldots \\ -\frac{1}{\Delta t} - \frac{\mu}{2}\frac{\partial F(x_2, \lambda_2)}{\partial x_1} & \frac{1}{\Delta t} - \frac{\mu}{2}\frac{\partial F(x_2, \lambda_2)}{\partial x_2} & 0 & 0 & \ldots \\ 0 & -\frac{1}{\Delta t} - \frac{\mu}{2}\frac{\partial F(x_3, \lambda_3)}{\partial x_2} & \frac{1}{\Delta t} - \frac{\mu}{2}\frac{\partial F(x_3, \lambda_3)}{\partial x_3} & 0 & \ldots \\ 0 & 0 & -\frac{1}{\Delta t} - \frac{\mu}{2}\frac{\partial F(x_4, \lambda_4)}{\partial x_3} & \frac{1}{\Delta t} - \frac{\mu}{2}\frac{\partial F(x_4, \lambda_4)}{\partial x_4}  & \ldots \\ \ldots & \ldots & \ldots & \ldots & \ldots  \end{array} \right)$

The determinant of the Jacobi matrix is merely a products of the diagoal terms

$\det \left(\frac{\partial \xi_i}{\partial x_j}\right) =\left(\frac{1}{\Delta t}\right)^N \prod_{i=1}^N \left(1- \frac{\Delta t\mu}{2} \frac{\partial F(x_i, \lambda_i)}{\partial x_i}\right) \\ = \left(\frac{1}{\Delta t}\right)^N \exp\left[ \sum_{i=1}^N \ln \left(1- \frac{\Delta t\mu}{2} \frac{\partial F(x_i, \lambda_i)}{\partial x_i}\right)\right] \\ \approx \left(\frac{1}{\Delta t}\right)^N \exp\left[- \sum_{i=1}^N \left(\frac{\Delta t\mu}{2} \frac{\partial F(x_i, \lambda_i)}{\partial x_i}\right)\right]$

We thus have

$p[x(t)] = \det \left(\frac{\partial \xi_i(t)}{\partial x_j (t)}\right) p[\xi(t)] \\ = \left(\frac{1}{\Delta t}\right)^N \prod_{i=1}^N \exp\left[- \left(\frac{\Delta t\mu}{2} \frac{\partial F(x_i, \lambda_i)}{\partial x_i}\right)\right] \prod_{i=1}^N \left( \sqrt{\frac{ \Delta t}{4\pi D}}  e^{-\frac{\Delta t}{4D}\xi_i^2}\right) \\ = \prod_{i=1}^N \left(\frac{1}{4\pi D\Delta t}\right)^{N/2}  \exp\left[ -\frac{\Delta t}{4D}\sum_{i=1}^N \xi_i^2 -  \frac{\Delta t\mu}{2} \sum_{i=1}^N\frac{\partial F(x_i, \lambda_i)}{\partial x_i}\right]$

In the continuum limit, this reads

$p[x(t)] \propto \exp{\left[ -\frac{1}{4D} \int_0^t (\dot{x}-\mu F)^2 d\tau - \frac{\mu}{2} \int_0^t \frac{\partial F(x, \lambda)}{\partial x} d\tau \right] }$

Define the stochastic action as

$\mathcal{A}[x(t)] \equiv \frac{1}{D} \int d\tau L(x(\tau), \dot{x}(\tau); \lambda(\tau))$

with stochastic Lagrange function

$L(x(\tau), \dot{x}(\tau); \lambda(\tau)) \equiv \frac{1}{4}(\dot{x}-\mu F)^2 + \frac{\mu D}{2} \partial_x F(x, \lambda)$

The stochastic path integral measuring is then 

$\int d[x(t)] = \lim_{\Delta t \to 0, N \to \infty, N\Delta t = t} \left(\frac{1}{4\pi D \Delta t}\right)^{N/2} \prod_{i=1}^N \int_{-\infty}^\infty dx_i(t)$

which is a summation of all the trajectories within the time interval $[t_0, t]$, and can be calculated approximately by Stratonovich partition procedure. 

























