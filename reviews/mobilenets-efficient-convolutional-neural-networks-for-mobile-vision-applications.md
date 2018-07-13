# MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications
Andrew G. Howard, Menglong Zhu, Bo Chen, Dmitry Kalenichenko, Weijun Wang, Tobias Weyand, Marco Andreetto, Hartwig Adam

## Summary

Deep convolutional networks have reached state-of-the-art accuracy levels but they are still very resource hungry and can't be applied to small devices such as phones, FPGAs without loss in efficiency. The authors base their architecture on the technique called Depth-Seperable convolutions which reduces the total parameters and computations of the network drastically. The also introduce two parameters to further downsample the network by trading off accuracy linearly.

Key Contributions:

- Replacing normal convolutions that go through whole width of the input channels to produce each output channel with a Depth-Seprable convolutions which is a combination of convolution that seperately goes through each of the M input channels to produce M output convolutions and 1x1 convolutions afterwards.

- Usually a convolution operation applies filters and combines the output of all those filters in the same operation. Depth-seperable seperates both of them, into filtering op and combining op(1x1 conv).

- They introduce two parameters one multiplies with the number of output filters a layer can produce thus this parameter controls the overall width of the network reducing which, they show is better than reducing the depth of the network.

- Another parameter is the resolution of the input image, this reduces the spatial size of feature maps after each layer and thus the computation.

## Strengths:

- Seperating convoltion operation into two sub-operations allows us to add Batch Norm and ReLU after each sub operation, thus doubling the capacity of non-linearity and geralizablity in the network.

- The network outperforms another compressive networks squeezenet while using 22x less computation.

- This approach is also another way of leveraging dense convolutions since our current hardware is not very efficient in handling sparse matrices.

- A robust and natural way of compression, almost all current mobile startups are using a form of mobilenet.

- It can deliver similar results in object detection as well when used as the base network.

## Weakness: 
- Although they tried inception v-2 techniques that did not show much improvement, they did not even try other techniques such as of Resnets or DenseNets which would've been an interesting study.
