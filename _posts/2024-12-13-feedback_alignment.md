---
title: "Feedback alignment"
date: 2024-12-13
categories:
  - blog
tags:
  - algorithm
  - training
math: true
---

Assuming identity forward and backward network path, backprop requires the connection weight matrix to be Hermitain $\mathbf{W}^T_l = \mathbf{W}\_l$ for every layer.
This demand for symmetric connectivity between forward and backward propagation is called the weight transport problem {GROSSBERG198723}. 

Consider the case that the nonlinear activation function $\mathbf{f}(\cdot)$ is a ReLu, the backward error $(\mathbf{\delta}\_l)\_i = (\mathbf{e}\_l)\_i$ if $(\mathbf{a}\_l)\_i > 0$, and $0$ otherwise. 
Therefore, the value of backward error behaves like going through a $\mathbf{a}\_l$ gated ReLu function. 
We can generally write it as $\mathbf{\delta}\_l = \mathbf{g}(\mathbf{e}\_l, \mathbf{a}\_l)$. 
The backprop algorithm can then be understood as a mean to maximize the correlation between $\mathbf{\delta}\_l$ and $\mathbf{h}\_{l-1}$. 

The chain rule in Eq.~\ref{eq:backprop_update_rule} also requires the network to have precise knowledge of all the downstream synapses, any disruption of the connectivity or the unawareness of the computational details would break the error propagation. 

Empirical evidences have shown that retrograde transport operates on timescales that are orders of magnitude slower than forward propagating neural activity {harrisStabilityFittestOrganizing2008}, making backprop of error unlikely on the same transportation path. 

It has been demonstrated that fixed, random connectivity patterns $\mathbf{B}$, instead of precise symmetric connectivity $\mathbf{W}^T$, is sufficient for efficient learning. 

That is, the feedback weight matrix need not be $\mathbf{W}^T$, but a random matrix $\mathbf{B}$, with constraints $\langle \mathbf{e}^T \mathbf{W} \mathbf{B} \mathbf{e} \rangle > 0$, meaning the the error signal $\mathbf{B} \mathbf{e}$, lies within $90^\circ$ of the original backprog $\mathbf{W}^T \mathbf{e}$, or in other words, $\mathbf{B}$ pushes the nework in roughly the same direction as backprop would. 

This is called the feedback alignment {lillicrapRandomSynapticFeedback}. 
The local Hebbian-like updating rule is changed to 

$\Delta \mathbf{W}\_l = -\eta \left((\mathbf{B}\_{l+1} \mathbf{\delta}\_{l+1}) \odot \mathbf{f}'(\mathbf{a}\_l)\right) \mathbf{h}^T_{l-1}$

by replacing $\mathbf{e}\_l = \mathbf{W}^T_{l+1} \mathbf{\delta}\_{l+1}$ to $\mathbf{e}\_l = \mathbf{B}\_{l+1} \mathbf{\delta}\_{l+1}$. 


