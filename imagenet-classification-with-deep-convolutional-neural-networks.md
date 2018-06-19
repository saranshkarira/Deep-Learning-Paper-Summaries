# ImageNet Classification with Deep Convolutional Neural Networks 
Alex Krizhevsky, Ilya Sutskever, Geoffrey E. Hinton

## Summary
The paper proposes a novel architecture, AlexNet, which uses deep convolution networks for classification. The architecture while being several layers deep, is significantly less memory hungry than a fully connected network of equivalent depth while theoretically being only slightly worse. The network went on to win ILSVRC 2012 with a significant margin.

Key Contributions:

- Trained largest convolution network till date and performed far better than best results ever reported.
- The Data is augmented in two forms to fit the high model complexity. first generating crops and their reflections, second by altering intensities of RGB channels.
- Several techniques are implemented to improve the training speed of the networks authors used ReLU non-linearity and multi-GPU parallel training.
- To improve generalization and reduce overfitting, Local Response Normalization, Overlapping Pooling and especially DropOut is used.
- Cross-GPU communication introduces overhead and thus kept to bare-minimum only where it's needed.

## Strengths
- The network takes much less memory than an equivalent fully-connected layer while performing much better.
- The network is invariant to the location of the object in the image.
- Less parameters also result in faster convergence.

## Weakness/Notes

- The hyperparameters of the network such as stride, filter size etc are not optimized and rather taken arbitrarily based on intution.
- There is much room for improvement of the network by simply increasing depth of the network.