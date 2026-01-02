---
title: "Power spectrum, autocorrelation, and order parameter of reinforcement learning"
date: 2022-04-14
categories:
  - blog
tags:
  - algorithm
  - reinforcement learning
math: true
---

## Power spectrum and white noise 

The Fourier transform of a deterministic function is

$g(\nu) = \int_{-\infty}^\infty f(t)e^{-i 2\pi \nu t} dt$

with the inverse transformation

$f(t) = \int_{-\infty}^\infty g(\nu)e^{i 2\pi \nu t} d\nu $

e.g. the the delta-function is the Fourier transform of the constant function $f(t) = 1$ is $\delta (\nu) = \int_{-\infty}^\infty e^{-i 2 \pi \nu t}dt$. 

The power of the signal is 

$E = \int_{-\infty}^\infty f^2(t) dt = \int_{-\infty}^\infty |g^2(\nu)|d\nu$

Thus, we can view $f^2(t)$ and $g^2(\nu)$ as the power densities in time and frequency domains, respectively.

The power spectral density is 

$|g^2(\nu)| = \int_{-\infty}^\infty f(t) e^{-i 2 \pi \nu t} dt \int_{-\infty}^\infty f(t) e^{i 2 \pi \nu t} dt \\ = \int_{-\infty}^\infty \left( \int_{-\infty}^\infty f(t) f(t-\tau) dt \right) e^{-i 2 \pi \nu \tau} d\tau  \\ = \int_{-\infty}^\infty \left( \int_{-\infty}^\infty f(t) f(t+\tau) dt \right) e^{-i 2 \pi \nu \tau} d\tau  \\ = \int_{-\infty}^\infty h(t,\tau) e^{-i 2 \pi \nu \tau} d\tau$

where $h(t, \tau) = \int_{-\infty}^\infty f(t) f(t+\tau) dt$. 

Now move on to stochastic process, we can view the sample path of a stochastic process as a function of time. Thus all the stochastic process is a random function such that its possible values are the sample paths. 
Fourier transformation can also be applied to the sample paths of the stochastic process, making the power also a random variable. 
The average is $\left<E\right> = \int_{-\infty}^\infty \left<|g^2(\nu)|\right>d\nu$, where 

$\left<|g^2(\nu)|\right> = \left< \int_{-\infty}^\infty f(t) f(t+\tau) e^{-i 2 \pi \nu t} dt \right> = \int_{-\infty}^\infty \left<  f(t) f(t+\tau) \right>e^{-i 2 \pi \nu t} dt $

Which is just the Fourier transform of the auto-correlation of the sample path at time $t$ and $t + \tau$. 
This is the informal expression of the Wiener-Khinchin theorem, which states the power spectral density of a wide-sense stationary stochastic process is the Fourier transform of the two-time auto-correlation function. 
Now we turn to the Wiener process, first we show that although Wiener process is continuous, it is not differentiable everywhere. 

The derivate $\xi(t) = \frac{dW}{dt} = \lim_{h \to 0} \frac{W(t+h) - W(t)}{h} = \lim_{h \to 0} \frac{W(h)}{h} \sim \frac{1}{\sqrt{h}} \to \infty$
We now prove that the auto-correlation of $\frac{dW}{dt}$ is actually a $\delta$-function since 

$\langle \xi(t) \xi(t+\tau) \rangle = \lim_{\Delta t \to 0} \langle \frac{W(t+\Delta t) - W(t)}{\Delta t} \frac{W(t+\tau + \Delta t) - W(t+\tau)}{\Delta t}\rangle \\ = \lim_{\Delta t \to 0} \langle \frac{W(t+\Delta t) - W(t)}{\Delta t} \rangle \langle\frac{W(t+\tau + \Delta t) - W(t+\tau)}{\Delta t}\rangle = 0$

$\langle\xi(t) \xi(t)\rangle = \lim_{\Delta t \to 0} \frac{\langle(\Delta W)^2\rangle}{(\Delta t)^2} = \lim_{\Delta t \to 0} \frac{1}{\Delta t} \to \infty$

so complete the proof $\langle \xi(t)\xi(t+\tau)\rangle = \delta(\tau)$. 

Now using the Wiener-Khinchin theorem, the spectrum of $\xi(t)$ is 

$S(\nu) = \int_{-\infty}^{\infty} \delta(t) e^{-i2\pi \nu t} dt = 1$. 

which means $\xi(t)$ contains arbitrarily high frequencies and thus having infinitely rapid fluctuations. And the spectrum contains equal amounts of all frequencies, thus it is referred to as ''white'', since the white light contains all kinds of colors (frequencies).
This also reveals the unrealistic of chosing Wiener process as the noise in stochastic differential equation since there is no such thing in physics having an infinitely high frequency of vibration. 
The reason that we can still model noise with Wiener process is that a differential equation is a filter that does not let through infinitely high frequencies. 
To understand this, we see $\langle x(t) x(t +\tau) \rangle$ is usually a wide peaked function, thus the bandwidth of its spectrum is 
narrower than $\langle \xi(t) \xi(t +\tau) \rangle$ which contains all the high frequencies. Thus a white noise will serve as a good approximation to 
real noise as long as the bandwidth of $x$ are much small compared to the bandwidth of frequencies of the real noise source. 

In short, white noise approximation is valid when the noise has a larger bandwidth of frequencies than the bandwidth of the system. 

## Edwards-Anderson (EA) order parameter
The intersections between Statistical Physics (specifically the study of Spin Glasses) and Reinforcement Learning (RL) is fascinating. 

In disordered systems (like spin glasses), the Edwards-Anderson (EA) order parameter, denoted as $q_{EA}$, 
measures the long-time autocorrelation of spins to distinguish a "glassy" (frozen, disordered) phase from a paramagnetic (random, fluctuating) phase.

$q_{EA} = \lim_{t \to \infty} \lim_{N \to \infty} \frac{1}{N} \sum_{i=1}^{N} \langle S_i(t_0) S_i(t_0 + t) \rangle$

### 1. Adaptive Exploration
In Deep RL, an agent can get stuck in a **local optimum**. 
In physics terms, the system has settled into a metastable state in a rugged energy landscape (similar to a spin glass ground state).
The Edwards-Anderson parameter can be used to measure the "frozenness" of the agent's policy or weights.
We calculate the autocorrelation of the agent's actions or the weights of the neural network over a time window.
If the agent is exploring randomly (Paramagnetic phase), it has low autocorrelation; while if the agent has converged, it has high $q_{EA}$. 
If the Reward is low but the Autocorrelation is high, the agent is trapped in a local minimum (a "glassy" state). 
We can use this signal to trigger a **"Phase Transition"**: 
increases the "Temperature" (exploration rate or entropy regularization) to "melt" the policy and allow the agent to escape the local trap.

### 2. Catastrophic Forgetting
One of the biggest problems in RL is **Catastrophic Forgetting** (learning a new task makes the agent forget the old one). 
This is mathematically analogous to the capacity limits of a Hopfield Network or a Spin Glass.
The replica overlap $q_{\alpha\beta}$ can be used to measures the similarity between the weight configuration required for Task A and Task B for an agent.
By monitoring these overlaps, algorithms (like *Elastic Weight Consolidation* or EWC) effectively construct a "potential well" that keeps
the system in a configuration that satisfies the frustration constraints of both Task A and Task B, preventing the system from drifting
too far (disordering) relative to the first task.

### 3. Episodic Memory
Hopfield Networks are energy-based models isomorphic to Ising Spin Glasses.
Since agents generally demands **Episodic Memory** to recall past states.
I may be possible to use the energy function of a spin glass to store environment states.
When the agent sees a new state, the network minimizes energy to "retrieve" the most similar past memory.
The retrieval strength is essentially the magnetization or overlap order parameter.
If the current state strongly correlates (autocorrelates) with a stored memory pattern,
the agent "remembers" the successful action taken in that past state.

In summary, the order parameter (autocorrelation) can be served as a **diagnostic tool for the loss landscape**:

1.  **High Autocorrelation + Low Reward:** We are in a Spin Glass phase (stuck in local optima). **Action:** Increase Temperature/Noise.
2.  **High Autocorrelation + High Reward:** We are in a Ferromagnetic phase (converged on a good solution). **Action:** Decrease Learning Rate.
3.  **Low Autocorrelation:** We are in a Paramagnetic phase (random walk). **Action:** Continue training to find order.
