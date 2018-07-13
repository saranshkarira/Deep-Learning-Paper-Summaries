# Deep Residual Learning for Image Recognition
Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun, arxiv, 2015

## Summary
One of the ways to make more powerful neural networks is to increase their depth, however, the deeper networks are more difficult to train. This paper's proposed architechture "ResNet", suggests adding residual functions as a solution. As a result, the authors were able to train a 152-layers deep network(8x deeper than VGG) which won ILSVRC'15.

Key Contributions:

- It is known that when a networks start converging, as the depth of network is linearly increased, the accuracy gets saturated and then degrades rapidly. While, overfitting seems an obvious culprit, the authors state that it is not so.
- They took a shallow network, and made it's deeper sibling by adding identity functions as the additional layers, since these layers are untrainable, If it were overfitting, the training error for both the networks should be same. However, results suggest otherwise.
- Solution : Let's take an arbitraty layer, X, in a stack of convoluions of a network. Usually, input to layer X+3 would be output from layer X+2. The paper suggests adding a parallel Shortcut/Skip connection from output of X and add it to the input of X+3.
- Mathmatically, it can be represented as a multiplication with an identity function before addition to the input.
- The authors hypothesize that, by adding skip connections, the output from layer X+2 becomes a residual, i.e. since, X is already serving as one of the input, the rest of the input only has to learn what has not been learned upto X, and thus in an ideal condition where there is nothing more to learn(The identity input is Optimal), the extra input is driven to zero, i.e the total input to X+3 becomes X, therefore the name "Residual learning" and this extra input function is called "residual".
- The authors also hypothesize that it is easier to learn residual layers than learning the whole unreferenced orignal function, since even if the X is non-optimal but still near to Optimal, very little has to be learned by the residual layers.


## Strengths 
- Appreciable Experiment work.
- Easy to optimize.
- It makes possible to train much more deeper models and as a result better accuracy.
- The skip connections can also be found in biological brains, this might suggest one possible reason of their existence.

## Weaknesses/Notes
- The dimensions of both skip as well as residual connections must be same, this restricts flexiblity in our network, to do so anyway linear projection is used which makes it less economical.
- While the conjectures made by authors seem plausible, lack of proper evidence hints to a possiblity that this may not be the case.
- No advantages were noticed when only single layer was skipped