# Network in Network
Min Lin, Qiang Chen, Shuicheng Yan

The authors propose a novel architecture to enhance model discriminalbility for local patches/ get a general representation of the underlying latent concept. They build 'micro-neural networks' of MLPs and slide these just like convolution filters to get feature maps. Also they replace Fully Connected layers with Global average pooling to tackle overfitting. The model demonstrates state-of-the-art performances on CIFAR-10/100

Key Contributions:

- Simple convolution filters are General Linear Models(GLM), their linearity makes them invariant to capture variations of the same concept(low abstraction). The authors suggest to replace GLMs with Multi-layer perceptron, since it introduces non-linearity and is a potent universal function approximator. The authors explain that these are able to capture general latent concepts, while GLMs can capture them as well, they'll need far more number of filters to achieve so.

- Fully Connected layers are black boxes, which makes it hard to interpret the signal passing between feature representation and categorization, also they are prone to overfit. These are overcome by replacing these with a Global 
Average Pooling layer, the number of final feature maps is equal to number of softmax categories,the average of each of the final feature map is taken and fed to softmax function, since there are no learnable parameters, network cannot overfit.

## Strengths
- The architecture is more discriminative due to non-linear nature.
- Global average pooling is less prone to overfit and easier to interpret.
- State-of-the-art performance on CIFAR 10/100.
- General representation of concepts need lesser number of parameters.

## Weakness/ Notes

- Since GAP is designed on categorical basis, it's tricky to fine tune the network on other datasets.
- No results on ImageNet data.
