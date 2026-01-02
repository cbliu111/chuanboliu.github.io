---
title: "Predictive coding and prospective configuration"
date: 2024-11-24
categories:
  - blog
tags:
  - algorithm
  - training
math: true
---

## Predictive coding

Predictive coding model suggests the brain constantly compares its predictions with actual sensory input. Feedback connections carry predictions down the hierarchy, while feedforward connections carry any discrepancies (errors) back up. This dynamic process allows the brain to refine its internal model and efficiently process sensory information {raoPredictiveCodingVisual1999}.
Functional MRI (fMRI) and EEG studies have shown that brain activity often reflects prediction errors. For example, unexpected stimuli tend to elicit stronger neural responses, which aligns with the idea that the brain is signaling a prediction error. MMN is elicited when there is a deviation from a predicted auditory pattern, supporting the idea that the brain is constantly making predictions about sensory input. 
It was shown that the predictive coding converges asymptotically (and in practice rapidly) to exact backprop gradients on arbitrary computation graphs using only local learning rules {millidgePredictiveCodingApproximates2022}.

Predictive coding is based on the assumption that brains implement an internal generative model of the world {fristonFreeenergyPrincipleUnified2010}. 

Learning happens by updating internal neural activities and synapses to minimize the prediction error. 
In computational models, this is done via a minimization of the variational free energy, in this case a function of the total error of the generative model. 
This minimization happens in two steps: first, internal neural activities are updated in parallel until convergence; then, synaptic weights are updated to further minimize the same energy function.

## Prospective configuration

And a similar learning principle, named prospective configuration, was proposed for predictive error assignment by first balance the activities and then update weights to consolidate the activity configuration {songInferringNeuralActivity2024}.

So, what's the difference between prospective configuration and predictive coding?

In current ANN, activity of neuron $x_i$ is determined by its inputs, $x_i^l = \sum_j \omega_{ij}^l x_j^{l-1}$. $i$ and $j$ represent neurons in different layers $l$. 
On the contrary, for energy-based networks, the activity of neuron $x_i^l$ is determined by an energy function $E_{ij}^l = \epsilon (x_i^l, \omega_{ij}^l, x_j^{l-1})$. 
When perform inference, connection weights $\omega_{ij}^l$ are fixed, input layer activity is clamped by the sampled data, and the network activities evolves to minimize the total energy $E = \sum_l \sum_{i,j} E_{ij}^l$. 

$\delta x_i^l = - \gamma \frac{\partial E}{\partial x_i^l} = - \gamma \sum_j \frac{\partial \epsilon (x_i^l, \omega_{ij}^l, x_j^{l-1})}{\partial x_i} - \gamma \frac{\partial \epsilon (x_k^{l+1}, \omega_{ij}^{l+1}, x_i^{l})}{\partial x_i^l} $. 

If $\epsilon (x_i^l, \omega_{ij}^l, x_j^{l-1}) = \frac{1}{2} (x_i^l - \omega_{ij}^l x_i^l x_j^{l-1})^2 $, this energy function corresponds to the fully-connected MLPs. 

This is called relaxation {songInferringNeuralActivity2024}. 
For training, first clamp both the input and output activities, and relax until equilibrium $x_i = x_i^*$. 
Then update the weights according to a gradient descent on the local energy $\delta \omega_{ij} = - \alpha \frac{\partial E}{\partial \omega_{ij}}$. 

This seems like a constraint optimization problem: minimize $E$, subject to $x_i^l = \sum_j \omega_{ij} x_j^{l-1}$. 
The number of constraint equations is the same as the number of neurons, so Lagrange multiplier is not applicable. 

Prospective configuration search for an energy minimum by updating the activities and weights separately. 
The form of energy tends to align all the neurons with the same activity. 
This form of energy is like the spin-wise interactions in Ising model, change of one spin cause diffused and limited influence on the network. 
Image the input activity is a sine wave, then the propagation of this wave along the layers (relaxation as in prospective configuration) is like a filter. 
High frequency signals are dropped because of the neuron-neuron interaction $x_i^l = \sum_j \omega_{ij} x_j^{l-1}$. 

The problem of prospective configuration is the training is inefficient for current computational devices, like GPU. It is more suitable for asymptotic computational devices, non-von-Neumann machines, such as analog chips, which updates its own weights independently. 

