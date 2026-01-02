---
title: "Stochastic integral and hindsight-foresight planning"
date: 2022-04-14
categories:
  - blog
tags:
  - algorithm
  - reinforcement learning
math: true
---

## Stochastic integral 

First consider the summation of independent identical Gaussian distributed random variables $W=\sum_{i=0}^N \Delta W_i$. 
We know $W$ is also Gaussian distributed with mean $\left<W\right>=\sum_{i=1}^N \left<\Delta W_i \right> = 0$, and variance $V(W)=\sum_{i=1}^N V(\Delta W_i) = N \sigma^2$. 

By setting $\sigma^2 = \Delta t$ (scaling of Brownian motion, the very fundamental property for all stochastic processes) we discover the Wiener process, which is formally defined as

1. $W(t)$ is continuous in (almost) every realization;
2. increments of $W(t)$ are independent on disjoint time interval;
3. each increment is Gaussian distributed with mean 0 and variance $\Delta t$;

To see why the variance is on the first order of time, consider the variance of $W(t)$

$V(W(T)) = \lim_{N \to \infty} \sum_{i=0}^{N-1} V(\Delta W_i) = \lim_{N \to \infty} \sum_{i=0}^{N-1} \Delta t^\alpha =  \lim_{N \to \infty} N \left(\frac{T}{N}\right)^\alpha = \lim_{N \to \infty} N^{1-\alpha}T^\alpha$

which is 0 for $\alpha > 1$, and $\infty$ for $\alpha < 1$, so not well-defined for a process. 

For Wiener process, we have for the infinitesimal increments

$\langle dW \rangle = 0$

$V(dW) = dt$

$\langle dW_m dW_n \rangle = \delta_{m,n} dt$

The last one can be verified from the independence of the increment and the Gaussian distribution of $dW$. 

Wiener process can be viewed as an integral of the infinitesimal Gaussian increments by the following sense (Ito stochastic integral)

$W(T) = \lim_{N \to \infty} \sum_{i=0}^{N-1} \Delta W_i \equiv \int_0^T dW(t)$

In this view, $W(T)$ is also Gaussian distributed with moments

$\langle W \rangle = 0$

$\langle W^2 \rangle = T$

$V(W) = T$

Assuming $t < s$, we have 

$\left< W_t W_s \right> = \left< W_t (W_s - W_t + W_t)\right> \\ = \left<W_t(W_s-W_t)\right> + \left<W_t^2\right> \\ = \left<(W_t-W_0)(W_s-W_t)\right>+\left<W_t^2\right> = t$

Therefore, $\langle W_tW_s \rangle =\min(s,t)$

Wiener process also has self-similarity since the mean is always equal and the variance is invariant under the scale transformation

$V(W_t)=V(\lambda^{-1/2} W_{\lambda t}) = 1/\lambda V(W_{\lambda t}) = t$

The existence of Wiener process is guarenteed by Kolmogorov extension theorem. 
Wiener process represent a continuous but still infinitly fluctuated process: small changes happen all the time, and smoothly. 
To understand why increment is Gaussian distributed, we can rely on the Central Limit theorem which states summation of independent identical distributed random variables with finite variance will approaches Gaussian distribution. 
If the transition time scale of noise is much smaller than the time interval $dt$ (also infinitesimal), which represented a time-scale separation, thus within $dt$ there will be an infinite many of contributions of  noise, so comes the Gaussian distribution. 

For infinite variance increments, it is the Levy process. 
For not continuous case, where increment is not infinitesimal in time interval $dt$, it is the jump process, e.g. continuous time Markov chain. 
We then show the most significant fact about Ito stochastic integral. 

$\langle \int_0^T (dW)^2 \rangle = \int_{-\infty}^\infty \left[ \int_0^T (dW)^2 \cdot P(dW) \right] dW \\ = \int_0^T \int_{-\infty}^\infty (dW)^2 P(dW) dW = \int_0^T \langle (dW)^2 \rangle = \int_0^T dt = T$

We can also show that $V\left(\int_0^T (dW)^2 \right) = 0$ and $P\left(\sum_{n=0}^{N-1} (dW)^2\right) = \delta \left(T - \sum_{n=0}^{N-1} (dW)^2\right)$. 

see Jacobs, K. (2010). "Stochastic Processes for Physicists_ Understanding Noisy Systems." Cambridge University Press.

Thus, we have $(dW)^2 = dt$ in the continuum limit. 

By Levy-Khinchine theorem, we can actually construct any continuous random process with independent increment from a Wiener process. For doing this, we need the Ito formula for transforming of representation of random variables. 
To preform Ito formula, since $(dW)^2 = dt$, we we should keep every term on order less than $dt$, and drop other high order terms. That is, we keep $dW$, $dt$ and $(dW)^2= dt$. 

That is, we expand the random variable to first order of time with respect to time and original random variable.
Assume $y = g(t, x)$, then 

$dy = \frac{\partial g}{\partial t} dt + \frac{\partial g}{\partial x} dx + \frac{1}{2} \frac{\partial^2 g}{\partial x^2} (dx)^2$

e.g. if $dx = fdt + gdW$, $y = x^2$, we have 

$dy = 2x dx + (dx)^2 = (2xf + g^2) dt + 2xgdW$

Now we can solve a real problem, the Ornstein–Uhlenbeck process. 

$dx = - \gamma x dt + g dW$

It is a linear differential equation driven by additive noise, where additive noise means the noise does not itself depend on $x$, but is merely added to any other terms that appear in the equation for $x$. 

We can solve this by the technique of ''changing variable'', $y = x e^{\gamma t}$, then 

$dy = e^{\gamma t} dx + x \gamma e^{\gamma t} dt = e^{\gamma t} dx + \gamma y dt = \gamma y dt + e^{\gamma t} (-\gamma x dt + gdW) \\ = ge^{\gamma t} dW$

The solution is the stochastic integral $y(t) = y_0 + g\int_0^t e^{\gamma s} dW(s)$, which has the general form 

$I(t) = \int_0^t f(s)dW(s) = \lim_{N \to \infty} \sum_{n=0}^{N-1} f(n \Delta t) \Delta W_n$

The mean is $\langle I(t) \rangle = \int_0^t f(s) \langle dW(s) \rangle = 0$, and variance $V(I(t)) = \int_0^t V(f(s)dW(s))=\int_0^t f^2(s) V(dW(s)) = \int_0^t f^2(s) ds$. 
Therefore, $V(y(t)) = g^2 \int_0^t e^{2\gamma s} ds = \frac{g^2}{\gamma} ( e^{2\gamma t} -1)$. 

We can also solve equation like $I = \int_0^t W dW$ by defining $y = \frac{1}{2} W^2$, we have 

$dy = WdW + \frac{1}{2} (dW)^2 = W dW + \frac{1}{2} dt = d\left(\frac{1}{2}W^2\right)$, which gives $I = \int_0^t W dW = \frac{1}{2} (W(t)^2 - t)$. 

## Hindsight-foresight planning

The relationship between a stochastic integral and accumulated rewards is fundamental in fields like Reinforcement Learning (RL), continuous-time finance, and control theory.

At its core, accumulated reward in a continuous-time setting is mathematically modeled as a stochastic integral.

Imagine we are driving a car on a bumpy road (a stochastic environment).
The Reward Function $r_t$: This is how much "points" or value we are getting at any exact split-second (e.g., speed, staying in the lane, fuel efficiency). 
This value fluctuates randomly because of the bumps.
The Accumulated Reward $R$: This is the total score we have at the end of the trip.
In discrete time (step-by-step), we just sum the rewards: $R = \sum_t r_t$. 
In continuous time, we integrate over the path. 
Because the path is noisy (random), this integration becomes a stochastic integral.

If the reward process involves randomness (Brownian motion or noise), the standard Riemann integral is insufficient, 
and we use stochastic calculus (Itô calculus).
The accumulated discounted reward $V$ over an infinite horizon is represented as:

$V=\mathbb{E} \left[\int_0^\infty e^{-\rho t} dR_t \right]$

Where $e^{-\rho t}$ is the continuous discounting factor, which represents the differential of the reward process.

The "Stochastic Integral" part is critical because:
* **Martingale Property:** The expectation (average) of an Itô stochastic integral is zero.
This means that while the noise makes the actual realized reward unpredictable,
the expected accumulated reward is determined entirely by the drift component
* **Variance/Risk:** While the stochastic integral doesn't change the average reward, it dictates the variance of the reward. In RL and Finance, this is the "risk."
A policy might maximize the drift (high return) but have a massive stochastic integral term (high volatility/risk), making it unstable.
* **Hamilton-Jacobi-Bellman (HJB) Equation**: In continuous-time RL (or optimal control), we don't use the Bellman equation (which uses sums). We use the HJB equation,
which is derived using Itô's Lemma (the fundamental rule of stochastic calculus) to handle these stochastic integrals.

To design an agent that thinks like a human—weighing a long history against a long-term future—
we are effectively trying to balance **Hindsight (Memory/Experience)** with **Foresight (Planning/Prediction)**.

In standard Reinforcement Learning (RL), agents are typically "Markovian"—they only care about the *current* state. 
They forget exactly how they got there (past) and compress the entire future into a single value estimate (future).

To break this and create the "Long Past / Long Future" dynamic we want, we need to move beyond standard value functions. 

### 1. The Mathematical Balance: The "Past-Future" Objective

Standard RL maximizes just the future: $G_t = \text{Future Rewards}$.
To include the past, we need a **Bi-directional Value Function**.

We can define our agent's objective function ($J$) not just as "what will I get," but "how does this fit my life story?"

$J = \lambda_{past} \sum_{k=1}^{\infty} \gamma_{P}^k r_{t-k} + \lambda_{future} \sum_{k=0}^{\infty} \gamma_{F}^k \hat{r}_{t+k}$

*   **Retrospective Utility (The Past):** This measures *consistency* or *regret*. "Does the action I am about to take honor the investments I made in the past?"
*   **Prospective Utility (The Future):** This is standard expected return. "Will this action lead to a good outcome?"
*   **$\lambda$ (Lambda):** These are our balancing weights. A high $\lambda_{past}$ makes the agent "traditionalist" or "stubborn" (sticking to past commitments). A high $\lambda_{future}$ makes the agent "opportunistic."

### 2. Architectural Implementation

We cannot achieve this with a simple Q-table or basic Deep Q-Network. We need specific architectures for "Long Past" and "Long Future."

#### A. Handling "Very Long Past" (Episodic Memory)
Standard Recurrent Neural Networks (LSTMs) fail at "very long" sequences (they forget after ~1000 steps). We might need **Episodic Memory**.

*   **Technique:** **Differentiable Neural Computer (DNC)** or **Transformer-XL**.
*   **How it works:** Instead of compressing the past into a hidden state vector, the agent stores raw snapshots of past experiences in an external memory bank.
*   **The "Human" Aspect:** Before taking an action, the agent queries this database. "Have I been in a situation like this 5 years ago? What did I do? Was it worth the effort?" This allows the agent to recall specific lessons from the distant past rather than just vague heuristics.

#### B. Handling "Very Long Future" (Hierarchical Planning)
Predicting the raw future 1,000 steps ahead is mathematically impossible due to compounding errors (variance explosion). Humans solve this via **Hierarchy**.

*   **Technique:** **Hierarchical Reinforcement Learning (HRL)** (e.g., Feudal Networks or the Options Framework).
*   **How it works:**
    *   **The Manager (Future Thinker):** Operates on a slow timescale. It sets abstract goals (e.g., "Get a PhD") that take years. It doesn't care about the muscle movements of walking to the library.
    *   **The Worker (Immediate Actor):** Operates on a fast timescale. It tries to fulfill the Manager's goal by handling immediate motor control (e.g., "Walk to library").
*   **The Balance:** The Manager predicts the "Very Long Future" (Strategic Value), while the Worker executes based on immediate feedback.

### 3. The "Sunk Cost" Mechanism (Meta-Cognition)
Humans balance past and future often through the **Sunk Cost Fallacy** (which can actually be rational in a resource-constrained environment).

To model this, we can introduce a **Credit Assignment** mechanism that penalizes changing strategies if the "Accumulated Reward" for the *current* strategy was high, even if the *Predicted Reward* for a *new* strategy looks slightly better.

**The Algorithm: Hindsight Experience Replay (HER) + Forward Modeling**

1.  **The Past (HER):** The agent looks at failed past trajectories and pretends they were successful goals. This fills its "Long Past" memory with useful data even from failures.
2.  **The Future (MCTS/World Models):** Use a model-based approach like **MuZero** or **World Models**. The agent simulates the future in a "dream" state (Monte Carlo Tree Search) to see deep into the future.

### 4. Summary: The Blueprint

To build this very agent, we need to combine three specific modules:

| Component | Function | Technology Solution |
| :--- | :--- | :--- |
| **Long Past** | "Do I remember doing this?" | **Transformer (Attention Mechanism)** over a history buffer. It allows the agent to "attend" to specific past events relevant to the current context. |
| **Long Future** | "Where does this lead?" | **Model-Based RL (World Models)**. The agent runs a simulation inside its head to predict outcomes hundreds of steps away. |
| **The Balancer** | "Is it worth changing course?" | **Meta-Controller**. A small network that outputs a scalar value $\alpha \in [0,1]$ weighting the Past Attention vs. the Future Prediction based on uncertainty. |

**The "Human" Heuristic:**
If the **Future** is uncertain (high entropy in prediction), the agent should rely heavily on the **Past** (conservative behavior). If the **Past** offers no similar situations (novelty), the agent must rely entirely on **Future** prediction (exploration).
