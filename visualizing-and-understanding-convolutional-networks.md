# Visualizing and Understanding Convolutional Networks

Matthew D. Zeiler, Rob Fergus, Arxiv,2013	

## Summary	

This paper introduces a novel approach to analyse the dynamics of intermediate layers of a convolutional neural networks. Upto this point,
 we only knew what happens in the first layer of a convolutional network, i.e. formation of low level representations but were completely unaware of
 the activities taking place in the deeper, hidden layers. Authors used their previously proposed DeconvNet to accomplish this and thus, by the analysis they fine tuned hyper-parameters of the Alexnet, This new network called ZFnet won ILSVRC'13

Key Contributions :

- To visualize the representations of any layer, the feature activations are used to reconstruct the input signal by putting other activations to zero.
- Each and every operation upto this layer in the forward pass of Convnet is reversed in the Deconvnet, the feature activation being it's input, while reconstructed image, it's ouput.
- There are 3 basic operations in Alexnet's convolution layers, Convolution, ReLU and Max-Pooling. 
-- The reversal of Convolution is done by simple convolution on the extended input(introduing 0's between each input element and zero padding) using the same filters and then transposing the resultant matrix(horizontal+vertical flip).
-- The reversal of ReLU is also a ReLU.
-- The reversal of Max-pooling is unpooling, which is approximated by using Switch Variables to remember the positions of Max-pooled activations and thus are different for each image.
- Well-designed experiments were perform to get the insights.

## Strengths:
- Observations of feature evolution
-- The lower layers converge within the first few layers, however, the intermeditate layers need a considerable amount of epochs(40-50).

- Feature invariance
-- The lower layers are dramatically effected with small transformations in the input image, while the higher layers show a very little impact. The model is fairly invariant to scaling and translation but not so much to rotation, however authors suggest that rotating the activations of the max-pooled layers might allow the network to learn such invariance as well.

- Sensitivity analysis using occlusion
-- Parts of image were occluded in parts and the following activations were analyzed. The activities drop significantly when the object is occluded, and intuitively, occluding other objects tend to increase the confidence of the ground truth class.
-- The network also tends to learn the features that do not corresponding to any of the orignal classes but are still present in the images. This is assumed due to high correlation among the objects in the real world(For example a necklace is most likely to be seen around a person's neck) and this correlantion tends to bind the confidence of one object's presence to other object as proven by the occlusion experiments.

Implicit Correspondence

-- The network learns implicit correspondence between the different parts of the object, this is shown by the fact that when the same parts of a front facing dog in multiple images were occluded, the difference in the activity drop was similar among all of them.

- The great performance as well as generalization as compared to similar but randomly initialized Alexnet shows the importance of hyperparameter tuning.

## Weakness/Notes:

- The suggestion for rotation worths looking into, while I'd prefer more if this invariance is learnt implicitly.
- Why does removing layer 7 improve top-1 error rate.
- The intuition for the choice of smaller filters wasn't convincing enough.
