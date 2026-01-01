---
title: "Weighted stochastic simulation algorithm"
date: 2022-04-26T10:18:30
categories:
  - blog
tags:
  - algorithm
  - stochastic simulation
mathjax: true
---

The stochastic behavior of a chemical system is typically described by a chemical master equation under the Markovian assumption. The chemical master equation is equivalent to a continuous time Markov chain in the discrete phase space that is constructed by the number of molecules of each species. A chemical reaction is then a random walk in this phase space while the transition probability matrix is completely determined by the system properties. 
Weighted stochastic simulation is nothing more but application of importance sampling in stochastic simulation. The application of rejection sampling in stochastic simulation of chemical reactions is called RSSA (Thanh, V. H., C. Priami and R. Zunino (2014). "Efficient rejection-based simulation of biochemical reactions with stochastic noise and delays." J Chem Phys 141(13): 134116.)

Given reaction $R_j$, stochiometric vector $v_j$, propensities $a_j(X(t))$, the time interval of jumps is exponentially distributed and the probability of chosen reaction \(R_j\) is \(\frac{a_j(X(t))}{a_0}\), where \(a_0 = \sum_j a_j\). 

The joint probability of reaction \(R_j\) occurs at time interval \((t + \tau, t + \tau + d \tau)\) is therefore

\[ P\{R_j, (t + \tau, t + \tau + d \tau)\} = a_j e^{-a_0 \tau} = \frac{a_j}{a_0} \times a_0 e^{-a_0 \tau} = P\{R_j\} P\{(t + \tau, t + \tau + d \tau)\} \]


Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
