# R-FCN: Object Detection via Region-based Fully Convolutional Networks
Jifeng Dai, Yi Li, Kaimang He, Jian Sun

## Summary

The RCNN family is known for doing redundant computation, due to the unshared computation after the ROI-pooling, authors suggest that this is due to the need of translation invariance in classification v/s translation variance in detection which serves a great dilemma. The authors use position-sensitive score maps which lets them use fully convolutional networks on a region based detector with almost no shared computation.

Key Contributions:

-The paper builds on Faster RCNN, works for increasing its speed while retaining it's superior accuracy.

- It explains the translation invariance v/s variance dilemma between classification and detection respectively.

- Reasons this is why we need a addition subnetwork after ROI-pooling in RCNN networks, which makes network slow due to redundant computation.

- Proposes a position-sensitive ROI-Pooling which removes the need of additional convolutional ops after ROI-pooling thus no redundant computations.

- Design strategies:
 
    - The key idea is to divide each Region Proposal as a grid of equal KxK bins(say 3x3).

    - Now after the pure convolutions of the classification network ends, say a ResNet-101, remove any other type of layer, average pooling and a FC layer in this case.

    - Now add a randomly initialized 1x1 convolution layer right after the stripped ResNet. The output filters of which should be equal to (K x K) * (C+1), here C is the number of classes and +1 for backgound.

    - It means, we have (C+1) filters for each of the K^2 bins. The ROI-pooling is done from these filters.

    - For each bin of KxK Region Proposal, we pool the regions(only of that bin, not the whole Proposal) selectively only from C+1 filters designated to that bin.

    - Now the each of the bins essentially give score for possiblity of presence of each of the classes of being in that bin.

    - The scores of all the bins are averaged on per-class-basis, thresholded and sorted in a decreasing order to give a prediction.



## Strengths
- The network is 2.5-20x faster than the faster RCNN
- In terms of accuracy it's comparable at 83.6 with Faster RCNN at 85.6 mAP.

## Weakness

- The specifications of score maps should be more detailed rather than refering to the code.

- The convergence of the network break if K=1.

- The speed of the network is still around 5-6 FPS(170ms), still far from real-time object detection.