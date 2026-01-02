---
title: "Energy consumption in brain"
date: 2024-08-20
categories:
  - blog
tags:
  - theory
  - brain
math: true
---

Neural signaling and the postsynaptic effects of neurotransmitter release combined to account for 80\% of the brain's adenosine triphosphate (ATP) consumption {attwellEnergyBudgetSignaling2001}
Brain is 10 times more energy expensive per gram than muscle, it is just 2\% of the body's weight, but 20\% of its metabolic load {balasubramanianBrainPower2021}. 
A coherent set of basic rules and learning as a principle of biological design where the brain ``saves only what is needed''{sterlingPrinciplesNeuralDesign2015}. 
Later study found communication between neurons is vastly more expensive than computation {levyCommunicationConsumes352021}. 

1969, Barlow introduced the phrase "economy of impulses" to express the tendency for successive neural systems to use lower and lower levels of cell firings to produce equivalent encodings. 
From this viewpoint, the ultimate economy of impulses is a neural code of minimal redundancy {10.1162/neco.1996.8.3.531}, which suggests that increased energy expenditure per neuron implies a decrease in average firing rate if energy efficient information transmission is to be maintained. 
These observations indicates a ``metabolic efficient'' manner of information process within the brain {10.1162/089976601300014358}. 

For neurons to transmit signals rapidly and efficiently across long distances within the nervous system, the neuron fires by altering their membrane potentials. 
When no stimulus is present, neurons have a resting membrane potential, typically around -70 mV, due to the distribution of ions inside and outside the membrane, such as sodium and potassium. 
When a neuron receives a signal from another neuron or a sensory input, it can cause a change in the membrane potential. 
If this change is strong enough to reach a certain threshold (usually around -55 mV), it triggers an action potential.
Once the threshold is reached, voltage-gated sodium channels open, allowing sodium ions to rush into the neuron. 
This influx of positive ions causes the membrane potential to become more positive, leading to depolarization.
The rapid depolarization causes the action potential to propagate along the axon of the neuron. 
This is an all-or-nothing event, meaning it either happens fully or not at all.
After the peak of the action potential, sodium channels close, and voltage-gated potassium channels open. 
Potassium ions flow out of the neuron, causing the membrane potential to become more negative and return toward the resting potential.
Sometimes, the outflow of potassium ions causes the membrane potential to become slightly more negative than the resting potential, a state known as hyperpolarization.
During and immediately after an action potential, the neuron enters a refractory period, during which it is less responsive to further stimulation. 
This ensures that action potentials only travel in one direction along the axon.
Ion pumps and channels restore the resting membrane potential, preparing the neuron to fire again if stimulated.

As a nonequilibrium system, the cell will has an intrinsic energy dissipation to maintain the resting membrane potential. 
Aside from that, the open and close of ion channels, pump of sodium-potasium ions to maintain ion concentration gradients, release of neurontransmitters at synapses and their subsequent reuptake or degradation also involve energy expenditure. 
In summary, the firing of neurons demands an inevitable energy dissipation. 

The energy dissipation rate is also dependent on the firing frequency. 
Stronger stimuli can increase the frequency of action potentials. 
Neurons encode the intensity of a stimulus by varying the rate at which they fire. 
A more intense stimulus can lead to a higher frequency of action potentials.
The absolute and relative refractory periods limit how quickly a neuron can fire again after an action potential. 
During the absolute refractory period, a neuron cannot fire another action potential, no matter how strong the stimulus. 
During the relative refractory period, a stronger-than-normal stimulus is required to initiate another action potential.
The frequency of firing can be influenced by the synaptic inputs a neuron receives. 
Excitatory inputs increase the likelihood of firing, while inhibitory inputs decrease it. 
The balance between these inputs affects the overall firing rate.
Different types of neurons have different intrinsic properties that affect their firing rates. 
For example, some neurons have ion channel compositions that allow them to fire rapidly, while others are more suited to slower firing rates.
Chemicals such as neurotransmitters and hormones can modulate the excitability of neurons, affecting their firing rates. 
For example, certain neurotransmitters can make neurons more or less likely to fire by altering ion channel activity.
Neurons can adapt to sustained stimuli by changing their firing rates over time. 
This adaptation can lead to a decrease in firing rate in response to a constant stimulus, allowing neurons to be more sensitive to changes in stimulus intensity.
In summary, the neuron firing frequency is determined by the identity of the neuron, the net intensity from both the excitatory and inhibitory inputs, and possible presentation of chemicals. 

As a simplified frequency model, we assume all the neurons are the same, and one single fire of each neuron costs the same energy dissipation. 
The energy dissipation of a single neuron is the product of the single fire energy cost and the frequency of firing. 
The frequency of firing is a function of the neuron output after activation function, which is determined by the forward passage and the backward passage. 
The overall energy dissipation is the summation of each neuron's energy dissipation. 

$E = \sum_l \sum_i (a_{l,i} - \theta)^2$

where $\theta$ is some overall threshold value for all neurons. 
This expression is very similar to Hinton's forward-forward algorithm, any deep connections? 
(Energy dissipation is the same of prediction goodness, indicate there is a deep connection between learning precision and energy consumption. 
For more precise learning, we need to dissipate more energy)





