---
title: "Large deviation and fluctuation relation"
date: 2024-01-10
categories:
  - blog
tags:
  - theory
  - field theory
math: true
---

We start with considering a sequence of two-state random events $\{x_i\}$ , the total observation number is $N$, it takes probability $r$ to be in the \#1 state and $1-r$ to be in the \#0 state. The number of observed \#1 is $n$, so the number of #0 is $N-n$. The average $f = n/N$ is an intensitive quantity that does not scales with $N$, while $n = \sum_{i=1}^N x_i$ 
is an extensive quantity that scales with $N$. 
The distribution of $n$ is of course a binomial distribution $P_N(n) = \binom{N}{n} r^n (1-r)^{N-n}$. 

Around the average $f$ this distribution can be approximated by the central limit theorem $P(f; N) \approx \sqrt{\frac{N}{2\pi r(1-r)}} \exp \left\\{-N\frac{(f-r)^2}{2r(1-r)}\right\\}$

We can check this by assigning $N=365$, $r=0.25$, $n=100$, and we obtain $P(\frac{100}{365}; 365) \approx 0.0270$, for binomial distribution.
And $P(\frac{100}{365}; 365) \approx 0.0267$ for central limit approximation.

However, if $n$ deviates from $fN$, e.g. $N=365$, $r=0.25$, $n=180$, we have $P(\frac{180}{365}; 365) \approx 9.94 \times 10^{-24}$ for binomial distribution.
And $P(\frac{180}{365}; 365) \approx 4.9 \times 10^{-27}$ for central limit approximation.

We then see a 3-order difference for the probability of this rare event. For improving the approximation of central limit theorem, we need the large deviation theory.
We define the rate function as $I(f) = - \lim_{N\to \infty} \frac{1}{N} \ln P(f; N)$ which is a rescaling logrithm transformation of the probability density function. We can write it in a more intuitive inspiring way, $P(f; N) \asymp e^{-NI(f)}$ which reads "the probability density function asymptotically approach $e^{-NI(f)}$". 

We can restore the Gaussian approximation by Taylor expansion of the rate function, which gives $I(f) \approx \frac{(f-\left<f\right>)^2}{2\hat{\sigma_f}^2}$, where $\hat{\sigma_f}^2 = \lim_{N \to \infty} N \sigma_f^2$, 
as the scaled variance of $f$. 

Next we introduce the relationship between the scaled cumulant generating function and the large deviation rate function.
The scaled cumulant generating function is 

$\psi^{(f)}(q; N) = \lim_{N \to \infty} \frac{1}{N} \ln \left<e^{qNf}\right> = \lim_{N \to \infty} \frac{1}{N} \Phi^{(f)}(q; N)$

as the name suggested, is the scaled version of the cumulant generating function

$\Phi^{(f)}(q; N) = \ln \left<e^{qNf}\right> = \ln \left<e^{qn}\right>$

We can obtain the average and variance surely from the scaled cumulant generating function

$\left<f\right> = \left.\partial_q \psi^{(f)}(q; N) \right|_{q=0}$

$\hat{\sigma}_f^2 = \left.\partial^2_q \psi^{(f)}(q; N) \right|_{q=0}$

And the Gartner-Ellis theorem says: if rate function is convex, then it is the Legendre-Fenchel transform of the scaled cumulant generating function, that is

$I(f) = \sup_q [qf - \psi^{(f)}(q; N)]$

and if this is the case, we can also recover the cumulant generating function from the rate function as

$\psi^{(f)}(q; N) = \lim_{N \to \infty} \frac{1}{N} \ln \int_{-\infty}^\infty df P(f; N) e^{Nqf} = \lim_{N \to \infty} \frac{1}{N} \ln \int_{-\infty}^\infty df e^{-N[I(f)-qf]} = \sup_f [qf - I(f)]$

We next show the application of large deviation technique in stochastic thermodynamics.
First, we introduce the static observables and the dynamic observables. Static observables are the functionals of the trajectory associated with the contributions of empirical dwell time.

$\mathcal{A}[x(t)] = \sum_y \alpha_y \tau_y$

where $\tau_y$ is the summation of time that trajectory remains at $y$: $\tau_y[x(t)] = \int_{t_0}^{t_f} dt \delta_{y, x(t)}^K$. 

Similarly, dynamic observables are functionals of the trajectory that associated with the contributions of empirical jump numbers

$J[x(t)] = \sum_{x \neq x'} n_{xx'}[x(t)] d_{xx'}$

where $n_{xx'}$ is the summation of jump numbers from $x'$ to $x$ within the observed trajectory

$n_{xx'}[x(t)] = \sum_{k=1}^n \delta_{xx_k}^K \delta_{x'x_{k-1}}^K$

and $d_{xx'}$ is antisymmetric, we say $J[x(t)]$ is an integrated empirical current. Typical empirical currents are:

* the entropy change of the heat reservoir $s^{res}[x(t)]$, corresponding to  $d_{xx'}=k_B \ln (k_{xx'}/k_{x'x})$
* the total entropy production $s^{tot}$, corresponding to $d_{xx'} = k_B \ln [(k_{xx'}p_{x'})/(k_{x'x}p_{x})]$

Integrated empirical current are then mostly associated with dissipation process, which are odd under time reversal transformation $(x(t) \to \hat{x}(t))$. 

The intensive counterpart of total entropy production is the empirical total entropy production rate $j_s^{tot} = \frac{s^{tot}}{\mathcal{T}}$, where $\mathcal{T}$ is the time duration of observation.

We assume the system is in nonequilibrium steady state condition, the integral fluctuation relation is then

$\frac{p(j_s^{tot}; \mathcal{T})}{p(-j_s^{tot}; \mathcal{T})} = e^{\mathcal{T}j_s^{tot}/k_B}$

We see that the empirical entropy total production rate follows a large deviation manner $p(j_s^{tot}; \mathcal{T}) \asymp e^{-\mathcal{T}I(j_s^{tot})}$

where the rate function $I(j_s^{tot})$ depends on the specific system. And hence we can write down the asymptotic detailed fluctuation relation as

$I(j_s^{tot}) - I(-j_s^{tot}) = \frac{j_s^{tot}}{k_B}$ 

If $p(j_s^{tot}; \mathcal{T})$ is Gaussian distributed, $I(j_s^{tot})$ is a parabola function, and we have $2k_B \left<j_s^{tot}\right> = \hat{\sigma}_{j_s^{tot}}^2$, where $\hat{\sigma}_{j_s^{tot}}^2$ is the scaled variance of the empirical total entropy production rate. This equation tells us about the relation between the mean and the scaled variance, and is another example of the fluctuation-dissipation relationship.
We can go further by applying Gartner-Ellis theorem to arrive at a more compact form of the asymptotic detailed fluctuation relation 

$\psi^{j_s} (q) = \sup_{j_s} [j_s q - I(j_s)] = \sup_{j_s} \left[j_s\left(q+\frac{1}{k_B} - I(-j_s)\right)\right] = \psi^{j_s}\left(-q-\frac{1}{k_B}\right)$

which revealed a symmetric transformation

$\psi(q) = \psi(-q - 1/k_B)$

valid for intensive observables obeying an asymptotic detailed fluctuation relation, which is often called the Gallavotti-Cohen symmetry.









