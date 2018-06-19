# Fast Image Scanning with Deep Max-Pooling Convolutional Neural Networks
Alessandro Giusti, Dan C. Ciresan, Jonathan Masci, Luca M. Gambardella, Jurgen Schmidhuber, 2013

## Summary
The conventional approach to Image Segmentation and dectection task using Deep CNNs is running the network in a sliding window approach through the image to detect the object patch, the authors argue that often most of these patches are overlapping and thus recomputing them each time is a waste of both time as well as computation. They approach it as a Dynamic Programming Problem and come to a solution that is several order faster than the conventional approach.

Key Contributions:

- Instead of generating several redundant feature maps per image patch, authors suggest it is rather better to produce a common set of feature maps for the whole image and extract our desired patches out of this set.
- While it is trivial in case of pure convolutions, it gets rather tricky while max-pooling is introduced, since they tend to miss the patches at odd coordinates and problem snowballs over as multiple such pooling layers are introduced.
- Authors suggest generating 'fragments' of feature maps, meaning each fragment is independent in the sense each one contains patches that do not exist in other fragments, union of these fragments contains all possible fragments of the image.

## Strengths
- Although overlapping pooling is an option, it gets really messy to extract desired patches from its feature map. This is a much cleaner and better approach.
- The speed gains are noticable by the mere fact that even its normal matlab implementation is 32.8 times faster than a the highly tuned GPU based implementation of the conventional technique.
- Seems like this paper served as a quite an inspiration for the YOLO framework.

## Weakness/ Notes
- A Pooling layer is used when we need to downsample the network, seems making so many fragments defeats the purpose but it is still downsampled when each patch is selected individually.
- While the approach is easy to comprehend, the explanation for the use-case was quite vague.
