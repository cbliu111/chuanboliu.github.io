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
