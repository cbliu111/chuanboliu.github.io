---
title: "Learning mechanism of biological neurons"
date: 2024-10-11
categories:
  - blog
tags:
  - theory
  - brain
math: true
---

Biological neuron fires or not depends on the summation of its inputs. 
There are both spatial summation and temporal summation. 
Spatial summation: signals from multiple simultaneous inputs. 
Temporal summation: repeated inputs. 
By adding up the individual inputs from temporal and spatial summation, if a threshold is met, the neuron fires. 

Biological neurons can adjust their synaptic weights, known as synaptic plasticity. 
Hebbian plasticity: "cells that fire together, wire together", the synaptic connection between two neurons is strengthened when they are activated simultaneous. This is a form of associative learning. (Maybe Hebbian rule is the result of some underlying learning mechanism)

Long-term potentiation (LTP): long-lasting increase in synaptic strength following high-frequency stimulation of a synapse {blissLonglastingPotentiationSynaptic1973}. 

Long-term depression (LTD): as the opposing process to LTP, LTD is a long-lasting decrease in synaptic strength. It occurs when neurons are activated out of sync or at low frequencies, allowing the brain to weaken less useful connections. 

Spike-Timing-Dependent plasticity (STDP): synaptic plasticity depends on the precise timing of spikes between pre- and post-synaptic neurons. If a presynaptic neuron fires just before a postsynaptic neuron, the synapse is strengthed. If it fires after, the synapse is weakened. (correlation is time-dependent, short-time range correlation leads to increase of weight, long-time correlation leads to decrease of weight)

Connection topology change: growth of new synapses or the pruning of existing ones. 

Sensitivity of sensor neurons will decay when facing constant strong input signal, this is self-adaptation. (This may due to the energy efficiency consideration.)

The brain uses feedback connections to induce neuron activities whose locally computed differences encode backpropagation-like error signals, this is called NGRAD (neural gradient representation by activity differences) {lillicrapBackpropagationBrain2020}. 

Some critical different features of BNN to ANN: 
* energy efficient: brain uses spikes, which is activated only when necessary, and the synaptic weights are only adjusted according to local information and sparsely in spacetime (lazy neuron); 
* no backpropagation: no fixed form of loss function, functionality of neurons in deep layers does not dependent on former layer neurons;
* modularity: damage of one part does not influence other parts;
* learn while inferencing: only forward computational process, no backward computational process, connection weights change constantly along with time and input data, learn all the time;
* global collective behavior from local interaction: neurons update weights only according to local information (there is no way they can have global sensibility), yet they form synaptic assemblies, given they only have local information;
* adaptability: learning new knowledge does not mean instantaneous forgetting the old knowledge; 
* few-shot learning capability: brain can learn through a very limited exposures to a stimulus; 
*  online learning: learn after each experience instead of a batch of experiences;
* curiosity: sensitive to unexpected or novel stimuli, 

Besides, these superiors, a human-like learning algorithm should also be efficient on the computational devices and can be easily scale up to train a very large model efficiently. 

It is very possible that the best learning algorithm for machine is different than the human brain. 
However, machine learning should inherit many of the good properties of human brain: energy efficient, modularity, online learning, continual learning, learning in changing environments (tasks), few-shot learning, etc. 
