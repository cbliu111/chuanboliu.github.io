---
title: "Weighted stochastic simulation algorithm"
date: 2022-04-26T10:18:30
categories:
  - blog
tags:
  - algorithm
  - stochastic simulation
math: true
---

## The weighted trajectory algorithm for stochastic simulation 

The stochastic behavior of a chemical system is typically described by a chemical master equation under the Markovian assumption. The chemical master equation is equivalent to a continuous time Markov chain in the discrete phase space that is constructed by the number of molecules of each species. A chemical reaction is then a random walk in this phase space while the transition probability matrix is completely determined by the system properties. 
Weighted stochastic simulation is nothing more but application of importance sampling in stochastic simulation. The application of rejection sampling in stochastic simulation of chemical reactions is called RSSA (Thanh, V. H., C. Priami and R. Zunino (2014). "Efficient rejection-based simulation of biochemical reactions with stochastic noise and delays." J Chem Phys 141(13): 134116.)

Given reaction $R_j$, stochiometric vector $v_j$, propensities $a_j(X(t))$, the time interval of jumps is exponentially distributed and the probability of chosen reaction $R_j$ is $\frac{a_j(X(t))}{a_0}$, where $a_0 = \sum_j a_j$. 

The joint probability of reaction $R_j$ occurs at time interval $(t + \tau, t + \tau + d \tau)$ is therefore

$$ 
P\{R_j, (t + \tau, t + \tau + d \tau)\} = a_j e^{-a_0 \tau} = \frac{a_j}{a_0} \times a_0 e^{-a_0 \tau} = P\{R_j\} P\{(t + \tau, t + \tau + d \tau)\}
$$

Introduce the diverged probability $b_j$ with $b_0 = \sum_j b_j$ of the one-step jump process given above, we have 
$$
P\left\{R_j, (t + \tau, t + \tau + d \tau)\right\} = a_j e^{-a_0 \tau} \frac{b_j/b_0}{b_j/b_0} = \frac{b_j}{b_0} a_0 e^{-a_0 \tau} \frac{a_j/a_0}{b_j/b_0}
$$
This is equivalent to choose the same jump according to probability $b_j/b_0$ with the same time interval distribution $p\left\{d\tau(t)\right\} = a_0 e^{-a_0 \tau}$ with an additional weighted factor $\omega_j = \frac{a_j/a_0}{b_j/b_0}$. 

The trajectory weight can be obtained from the Markovian property 
$$
\omega(j_1, j_2, \ldots, j_n) = \prod_k \omega_{j_k}
$$
Weighted trajectory is useful for approximate the first passage time distribution $P\left\{X_0, S; t\right\}$, which is the probability that the system starts at time $0$ in state $X_0$ will first reach state set $S$ at some time $\tau \le t$. 

$P\left\{X_0, S; t\right\}$ is the cumulative distribution of the first passage time, and the mean first passage time (MFPT) is calculated as
$$
\langle T(X_0, S) \rangle = \int_0^\infty t(dp\left\{X_0, S; t\right\}/dt) dt = \int_0^\infty (1 - p\left\{X_0, S; t\right\}) dt
$$

If using brute force simulation, $P\left\{X_0, S; t\right\} = \frac{m_n}{n}$. 

If using weighted trajectory simulation, $P\left\{X_0, S; t\right\} = \frac{\sum_i \prod_k \omega_{j_k}^{(i)}}{n}$.

The trick is, we can arbitrarily manipulate the trajectory weights to increase the summation with a fewer number of trajectories. Therefore, if we have some known proposal distribution about the true distribution, the weighted trajectory algorithm is very helpful in sampling rare events accurately for saddle points on the probability landscape defined as $U = - \ln P(X)$. 

In practical, to avoid the "infinite weight" problem of setting $b_j = 0$, we set $b_j = \gamma_j a_j$. 

So the problem becomes, how to chose $\gamma_j$ to best estimate the first passage time distribution?

It can be shown that the number of simulations to reduce the uncertainty of the first passage time distribution is related to the variance of the weighted samplings. 
Since the weight of each trajectory is an accumulation of many step-weights, we can approximate the weight distribution as a Gaussian distribution according to the central limit theorem, the sample variance 
$$
\sigma^2 = \frac{1}{n} \sum_k \omega_k^2 - \left(\frac{1}{n} \sum_k \omega_k\right)^2
$$
is associated with the uncertainty $\epsilon = \pm \frac{\sigma}{\sqrt{n}}$ and relative uncertainty $u = \epsilon/p$. And for ordinary stochastic simulation, each trajectory weight the same, $\hat{\sigma}^2 = (m_n/n)(1-(m_n/n))$, with uncertainty $\hat{\epsilon} = \pm \sqrt{\frac{(m_n/n)(1-(m_n/n))}{n}}$, and relative uncertainty, for rare trajectory $m_n/n \ll 1$
$$
\hat{u}=\pm \sqrt{\frac{1-(m_n/n)}{m_n}} \approx \pm \sqrt{1/m_n}
$$
If ordinary and weighted simulation has the same relative uncertainty, $u = \hat{u}$, denote the number of successful run in ordinary simulation as $\hat{m}$, we have $\hat{m} = \hat{p}\hat{n}$, and $\hat{n} = \hat{p}/\epsilon^2$, also $n=\sigma^2/\epsilon^2$, we have $g = \hat{n}/n = \hat{p}/\sigma^2$. 

So the gain of time reduction between ordinary and weighted stochastic simulations that needed to achieve the same relative uncertainty is related to the sample variance of the weighted simulation. 
An intuition of this idea comes from the observation that most 'successful' run will end up with a weight that very close to the average ratio thus resulted with a less scattered distribution of the trajectory weights. 

## For long-time reasoning and planning

Weighted trajectory stochastic simulation is still useful for generative AI, particularly for long-time reasoning and planning since we can treat the chain-of-thought and sequence-of-decision as a trajectory under the framework of reinforcement learning. 

This idea bridges classical statistical physics/simulation methods with modern Large Language Model (LLM) reasoning.

We are essentially proposing that we view an AI's reasoning process not just as token-by-token generation, but as a **path sampling problem** in a high-dimensional state space.

We can then apply **Weighted Trajectory Stochastic Simulation (WTSS)** to Generative AI reasoning and planning under an RL framework.

### 1. The Theoretical Mapping

To make this work, we first map the terminology of stochastic simulation to Generative AI:

*   **Particle/System State ($x_t$):** The current context window (the prompt + reasoning generated so far).
*   **Trajectory ($\tau$):** The entire Chain-of-Thought (CoT) or sequence of actions taken by an agent from start to finish.
*   **Reaction/Transition ($P(x_{t+1}|x_t)$):** The LLM's probability distribution for the next token or action.
*   **Weight ($w$):** The importance or validity of a specific reasoning path.
*   **Rare Event:** Successfully solving a very complex, multi-step logic puzzle or generating a novel scientific hypothesis (events that have low probability under standard random sampling).

### 2. Why Standard Generation Fails at "Long-Time" Horizons

In standard LLM generation (e.g., greedy decoding or nucleus sampling), errors accumulate. This is often called the **"Error Cascading"** problem.
If an LLM makes a small logical error at step 5 of a 100-step reasoning chain, the entire trajectory diverges from the solution. Standard RL (like PPO) tries to optimize the policy to avoid this, but it struggles with sparse rewards (you only know you failed after 100 steps).

### 3. Implementing Weighted Trajectory Stochastic Simulation

Here is how WTSS solves the "long-time" horizon problem in AI reasoning:

#### A. Importance Sampling for Reasoning
Instead of generating one path, we generate multiple reasoning paths. However, simply generating $N$ paths (Monte Carlo) is inefficient because the "correct" complex reasoning path is a *rare event*.

Using **Weighted Stochastic Simulation**, we can bias the generation toward promising directions and correct for the bias later using weights.
*   **The Bias:** We might use a "Value Model" (a critic) to steer the generation toward states that look like they are solving the problem.
*   **The Weight:** $W(\tau) = \frac{P_{target}(\tau)}{P_{biased}(\tau)}$.
*   **Result:** We explore high-reward regions of the reasoning space more thoroughly without losing mathematical rigor.

#### B. Trajectory Splitting and Enrichment (The "Go-With-The-Winner" Strategy)
This is directly inspired by methods like *RESTART* or *Splitting* in physics simulations.
1.  **Checkpointing:** At intermediate steps of the reasoning chain (e.g., after every paragraph of thought), we evaluate the quality of the trajectory.
2.  **Cloning:** If a partial thought process looks promising (high weight), we **split** it into multiple parallel branches to explore that logic further.
3.  **Pruning:** If a partial thought process looks incoherent (low weight), we kill that trajectory to save compute resources.
4.  **Outcome:** This concentrates computational power on the most likely "winning" trajectories, extending the effective planning horizon significantly.

### 4. Connection to Reinforcement Learning (RL)

In the RL framework (specifically Offline RL or Model-Based RL), this aligns with **Trajectory Optimization**.

*   **Policy $\pi_\theta(a|s)$:** The LLM generating the thoughts.
*   **Reward $R(\tau)$:** The correctness of the final answer or the coherence of the plan.
*   **Twist:** Instead of just updating weights $\theta$ (which is slow and expensive), we perform **inference-time optimization**. We treat the generation as a simulation where we want to estimate the expectation of success.

$$ \mathbb{E}[R] = \int P(\tau) R(\tau) d\tau \approx \sum_{i} w_i R(\tau_i) $$

By using weighted simulation, we can estimate the best plan without needing to retrain the model. We are essentially doing **Monte Carlo Tree Search (MCTS) on steroids**, using continuous weights rather than discrete visit counts.

### 5. Concrete Application: "Tree of Thoughts" (ToT) as Simulation

The popular "Tree of Thoughts" prompting strategy is actually a rudimentary form of this.
*   **Simulation:** ToT generates multiple candidate "thoughts."
*   **Weighting:** It asks the LLM to self-evaluate (vote) on those thoughts.
*   **Selection:** It keeps the high-weight paths.

**WTSS takes this further by:**
1.  Formalizing the weights mathematically (handling the probability ratio).
2.  Allowing for "soft" pruning (keeping low-probability paths alive but with low weights, to prevent mode collapse).
3.  Handling continuous state spaces better than discrete trees.

### Summary

WTSS is useful because **scaling compute during inference** is currently yielding better results than just scaling model parameters.

Weighted Trajectory Stochastic Simulation provides the mathematical control theory to guide an LLM through a "long-time" reasoning process (e.g., writing a novel, proving a theorem, coding a full app) by rigorously managing the probability of drift and ensuring the model converges on a high-reward solution.
