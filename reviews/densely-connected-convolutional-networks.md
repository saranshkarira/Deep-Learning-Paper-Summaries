# Densely Connected Convolutional Networks
Gao Huang, Zhuang Liu, Laurens van der Maaten, Kilian Q. Weinberger

## Summary

In this paper, inspired from shortcut connections in recent networks, authors connect feature maps of each layer to every subsequent layer. The resulting architecture, DenseNet, counter-intuitively uses a lot less parameters as well as computations while beating most of the state-of-the-art models at the same time.

Key Contributions: 

- Direct connections from any layer to every subsequent layer.
- Connections are concatenated unlike summation in Resnets, clearer information flow.
- Heavy feature reuse, since each layer can access all the maps before it.
- Each layer is directly connected to loss layer, hence more discriminative features are learned.
- Composite funtion - [BN > ReLU > 3x3 Conv] on every layer.
- Pooling layer - When layer size changes we use Pooling layer between the two blocks.
  [BN > 1x1 > 2x2 avg. Pool]  
- The no. of maps each layer produces is very narrow/low, this no. is called growth rate.
- BottleNeck layers - A flavor of DenseNet was trained using [BN > ReLU > 1x1conv > BN > ReLU > 3x3conv] instead of composite fxn.
- Compression : The 1x1 in Pooling layers is used for compression.
- Dropout was used on datasets where augmentation was not used.

## Strengths
- Feature reuse make it Smaller and Faster.
- The model gives better improvements with increase in both depth and width meaning it can utilize increase in representation power easily.
- Potential overfitting is countered by bottleneck and compression.

## Weakness
- Concatenating strategy of Inception and DenseNet is similar, could've used variable sized filters per layer to make it more width complete as well(Further parameter reduction?)

- Should've compared to an equally dense resnet styled connected net(Summation) to give a better comparision.

