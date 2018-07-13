# SqueezeNet: AlexNet-level Accuracy With 50x Fewer Parameters And <0.5MB Model Size
Forrest N. Iandola, Song Han, Matthew W. Moskewiez, Khalid Ashraf, William J. Dally, Kurt Keutzar, arxiv, 2016

## Summary

With an advent of deep neural network, comes a huge model size which makes it impractical for embedded applications such as FPGAs or regular OTA updates on self-driving cars. This paper focuses on significantly reducing the size of deep neural networks. 

Key Contributions:

- First paper to "explicitly" mention the modular approach and it's benefits(Yes, Inception was the first modular architecture).
- Authors propose that instead of tinkering each and every layer of a network which could scale to more than hundreds of layers, it is better to only design a local module(CNN Microarchitecture) and stack this module on top of one another along with some ad-hoc layers to make the overall network(CNN macroarchitecture) deeper.
- Design strategies :
	- Strategy 1. Replace majority of 3x3 with 1x1 filters to reduce parameter size by 9x
	- Strategy 2. Decrease the number of input channels to 3x3 fitlers using squeeze layers.
	- Strategy 3. Downsample late in the network to have large activation maps, which they intuit, increase classification accuracy.
- The squeeze layer is nothing but 1x1 conv filters, the way they squeeze is explained with Fire Modules.4
- Fire Modules : A fire module is the microarchitecture of SqueezeNet, It contains a squeeze layer and a subsequent Expand conv layer(combination of 1x1[Strategy 1] and 3x3 filters). The no of filters in squeeze layer is kept smaller than total number of filters in expand layer(Squeeze Ratio/0.125), thus squeezing/reducing the number of input channels using Strategy 2.
- Further compression strategies such as Network Pruning and Deep compression are applied from earlier papers of Han et al.


## Strengths 
- On ordinary computers, whole model can be loaded on primary cache levels during test time, making it faster.
- More efficient distributed training, small models require less communication.
- Less overhead during OTA updates to clients
- Feasable on FPGAs and embedded systems.
- The network was moreover an experiment to answer whether compression techniques be applied to smaller models without compromising accuracy, representational power.

## Weaknesses/Notes
- The squeeze approach in itself though effective, does not seem much impressive as pointed out by subsequent experiments in Incpetion V3-4 paper.