---
title: "Continuous Markov process and continual decision making"
date: 2022-04-14
categories:
  - blog
tags:
  - algorithm
  - reinforcement learning
math: true
---

A continuous time Markov chain can be viewed as a discrete time Markov chain with altered transition times. 

$P(X(s+t)=j \mid X(s)=i, X(r)=i_r, r \in \xi_s \subseteq [0, s)) = P(X(s+t)=j \mid X(s)=i)$

That is, the conditional probability distribution of $X(s+t)$ given all the history is coincide with the conditional probability distribution given $X(s)$. 
Markov property can be viewed as the ''future'' is independent of the ''past'' given the ''present'':

$P(X(s+t), X(r) \mid X(s)) = P(X(s+t) \mid X(r),X(s))P(X(r) \mid X(s))=P(X(s+t) \mid X(s))P(X(r) \mid X(s))$

For finite discrete state process, $P(X(s+t)=j \mid X(s)=i)$ are called the transition probability. 
If further assume homogeneous transition with a stationary transition probability, then 

$P(X(s+t)=j \mid X(s)=i)=P(X(t)=j \mid X(0)=i) \equiv P_{i,j}(t)$

Irreducible: there is a positive probability to get from any state to any other state at some finite time. 
For an irreducible continuous time Markov chain we have $\alpha_j \equiv \lim_{t \to \infty} P_{i,j}(t)$ not dependent on the initial state. 

For an aperiodic irreducible finite state Markov chain, the long time behavior converges to a stationary distribution. See e.g. Durrett, R. (2016). "Essentials of Stochastic Processes."

The Chapman-Kolmogorov equations

$P_{i,j}(s+t) \\ = P(X(s+t)=j \mid X(0)=i) \\ = \sum_k P(X(s+t)=j, X(s)=k \mid X(0)=i) \\ = \sum_k P(X(s)=k \mid X(0)=i)P(X(s+t)=j \mid X(s)=k,X(0)=i) \\ = \sum_k P(X(s)=k \mid X(0)=i)P(X(s+t)=j \mid X(s)=k) \\ = \sum_k P_{i,k}(s)P_{k,j}(t)$

We have used Markov property and homogeneous transition assumption in the last two equations.
C-K equations can be written compactly in matrix multiplication form $P(s+t)=P(s)P(t)$. 
Thus the transition function has a semi-group property because inverse transition is mission. 
The trajectory probability is then $P(j_1, j_2, \ldots, j_k) = \sum_{j_0}P(X(0)=j_0)P_{j_0,j_1}(t_1)P_{j_1,j_2}(t_2-t_1)\ldots P_{j_{k-1},j_k}(t_k-t_{k-1})$. 

We can understand continuous time Markov chain with discrete time Markov chain. Instead of having each transition take unit time, a continuous time Markov chain will have a random time for each transition. 
Given the memoryless of Markov property, we have $P(\tau+T \mid T)=P(\tau \mid 0)$. 
That is, the time distribution of transition of state $i$ is independent of how much time we have already spent at $i$. The only probability distribution that satisfied this property is the exponential distribution. 
Thus a continuous time Markov chain can be viewed as a discrete time Markov chain combined with a Poisson process which characterize the occurrence of transition between states along with time. However, the rate of the Poisson process is varied along with the trajectory. 

Another way of construction is through the transition rates $Q_{i,j} \equiv \frac{d P_{i,j}(0+)}{dt}$ with $P(0)=I$. 
So, $P_{i,j}(h)=Q_{i,j}h+o(h)$ as $h\downarrow 0$ for $i \neq j$, and $P_{i,i}(h)-1=Q_{i,i}h+o(h)$, where $-Q_{i,i}=\sum_{j, j\neq i} Q_{i,j} = \nu_i$. 

For doing this, we have to assume the transition probabilities are continuous at 0, then the derivatives exist. 
Forward C-K equation

$\frac{dP(t)}{dt}=\frac{P(t+h)-P(t)}{h}=\frac{P(t)P(h)-P(t)}{h}=P(t)\frac{P(h)-I}{h}=P(t)\frac{P(h)-P(0)}{h}=P(t)Q$

Backward C-K equation

$\frac{dP(t)}{dt}=\frac{P(t+h)-P(t)}{h}=\frac{P(h)P(t)-P(t)}{h}=\frac{P(h)-I}{h}P(t)=QP(t)$

The solution for both forward and backward C-K equation is the matrix exponential representation

$P(t)=e^{Qt} \equiv \sum_{n=0}^\infty \frac{Q^n t^n}{n!}$

The reason is that $Q$ and $e^{Qt}$ are actually commute

$\frac{d}{dt}\sum_{n=0}^\infty \frac{Q^n t^n}{n!}=\sum_{n=0}^\infty \frac{d}{dt} \frac{Q^n t^n}{n!}=\sum_{n=0}^\infty \frac{nQ^n t^{n-1}}{n!}=Q \sum_{n=0}^\infty \frac{Q^n t^{n}}{n!}=Qe^{Qt}$

We can also construct the continuous time Markov chain by assigning a random time to each transition which is distributed exponentially with rate $Q_{i,j}$

$P(\tau) = Q_{i,j} e^{-Q_{i,j} \tau}$

The actual transition happens with time $T_i \equiv \min_j \{T_{i,j}\}$. 

Since the minimum of several independent exponential random variables is again an exponential random variables with a rate equal to the sum of the rates, 

$P(T_i \le t) = 1-e^{-\nu_i t}$

And the probability of this transition is just transition of $i \to j$ is 

$P(N_i = j)=\frac{Q_{i,j}}{\sum_{k,k\neq i}Q_{i,k}}=\frac{Q_{i,j}}{\nu_i}$ 

for $i \neq j$. 

The joint distribution is then

$P(T_i \le t, N_i = j) = P(T_i \le t)P(N_i = j) = (1-e^{\nu_i t})\left(\frac{Q_{i,j}}{\nu_i}\right)$

Noted the above construction does not work for self-loop transition. But we can always transform a self-loop transition into an non-self-loop continuous time Markov chain. 
The transition probabilities are changed to $\hat{P}_{i,j}=\frac{P_{i,j}}{1-P_{i,i}}$, and to recover the rate matrix 

$\hat{Q}_{i,j} \equiv \hat{\nu} \hat{P}_{i,j} = \nu_i (1-P_{i,i})\frac{P_{i,j}}{1-P_{i,i}}=\nu_i P_{i,j}$

where $\hat{\nu} = \nu_i (1-P_{i,i})$. 

If the timers are nonexponentially distributed, we generalized the continuous time Markov chain to generalized semi-Markov process. 
At last we can construct the continuous time Markov chain through a unit rate Poisson process and a discrete time Markov chain, which is called uniformization. 
The trick is to introduce a self-loop transition probability to ensure 

$\nu_i = \sum_{j, j\neq i} Q_{i,j} \le \lambda$

then the self-loop transition probability is $1-\frac{\nu_i}{\lambda}$. Thus, in every state $i$, an independent thinning is required to recover the original continuous time Markov chain from the uniformized process. 
The transition probabilities become

$\tilde{P}_{i,j}=\frac{Q_{i,j}}{\lambda}$

$\tilde{P}_{i,i}=1-\sum_{j, j\ne i} \tilde{P}_{i,j}=1+\frac{Q_{i,i}}{\lambda}$

In matrix notation, $\tilde{P}=I+\lambda^{-1}Q$. 

The transition probability is then

$P_{i,j}(t) = \sum_{k=0}^\infty \tilde{P}_{i,j}^k P(N(t)=k) = \sum_{k=0}^\infty \tilde{P}_{i,j}^k \frac{e^{-\lambda t} (\lambda t)^k}{k!}$

We can verify the equivalence of uniformization process and the origin process. Since $\tilde{P}_{i,j}^0=0$ for $i \neq j$, and $\tilde{P}_{i,j}^0=1$ for $i = j$, 

$P_{i,j}(h)= \lambda h e^{-\lambda h} \tilde{P}_{i,j}^1 + o(h) = \lambda h e^{-\lambda h} \frac{Q_{i,j}}{\lambda} + o(h) = Q_{i,j}h + o(h)$

and 

$P_{i,i}(h)-1=(1-\lambda h + o(h)) + (\lambda h + o(h)) \left(1 + \frac{Q_{i,i}}{\lambda}\right) + o(h) - 1 = Q_{i,i}h + o(h)$

Both are consistent with the transition rates of the original proces. 
The uniformization process gives a proof of the exponential representation of the solutio of forward and backward C-K equations. 

$P(t) = \sum_{k=0}^\infty \tilde{P}^k \frac{e^{-\lambda t} (\lambda t)^k}{k!} = \sum_{k=0}^\infty (\lambda^{-1} Q + I)^k \frac{e^{-\lambda t} (\lambda t)^k}{k!} = e^{-\lambda t} e^{(Q+\lambda I)t} = e^{Qt}$

Existence and uniqueness of limiting probability distribution:
For an irreducible finite-state continuous time Markov chain, there exists a unique limiting probability vector such that $\alpha_j \equiv \lim_{t \to \infty} P_{i,j}(t)$ is stationary for all $j$ and $t > 0$. 







