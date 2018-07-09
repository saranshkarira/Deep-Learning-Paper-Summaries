# Overfeat : Integrated Recognition, Localization and Detection using Convolutional Neural Networks

Pierre Sermanet, David Eigen, Xiang Zhang, Michael Mathieu, Rob Fergus, Yann LeCun

## What is Overfeat?

The Overfeat paper proposes three things, 
- Multiple similar tasks can be integrated into one single network and while doing so, it also increases their overall accuracy(Accuracy of each task increases by integrating multiple tasks).

- They show an efficient way to apply multiple scales and sliding window approach.

- They also branch a bounding box predictor out of the network that uses multiple similar bounding box suggestions to predict the correct location. By using the box suggestions for predictions, Detection can be performed without training for the background class which let's network only focus only on positive classes for better accuracy.

The images of ImageNet roughly put the object in center, However, this may not be the case each time and for this their first idea is to apply ConvNet in multiple locations in a sliding window fashion at multiple scales.
Even after that, in many windows the portion of the object may be correctly identifiable but is not the entire object. While such windows produce a descent classification, it results in a very poor detection and localization. To tackle this they introduce a second idea of bounding box predictor branched out of the same network which gives a good prediction of the location as well as the size of the bounding box.
This dense sliding window method beats the conventional object proposal methods such as semantic segmentation on ILSVRC13 detection dataset.

The paper is divided into three categories based on the three vision tasks namely, classification, localization and detection

## Classification

The paper uses a network similar to Alexnet but with some improvements of their own, they've shown results on ILSVRC12 dataset i.e. 1.2 mill train pts and 1000 classes.
During training, the model uses fixed size inputs similar to AlexNet but turns to Multi-scale during classification. Each image is downsampled so that smallest dimension is 256 pixels, then similar to Alexnet subsamples out 5 random crops and their flips. The weights are initialized with zero-mean gaussian of     std_dev = 0.01. They are updated by SGD with momentum of 0.6 and L2 wt decay of 1x10^-5. The learning rate is initially 5 x 10^-2  and is successively decreased by a factor of 0.5 after required epochs. Similarly, dropout rate of 0.5 is also employed on 6th and 7th FC layer.

During training, we treat this architecture as non-spatial (producing 1x1 output maps ) as opposed to inference step, which produces spatial outputs. Layers 1-5 including "relu" and max pool are similar to Alexnet  but with following differences :              
           1) No contrast normalization 
           2) No overlapping in pools
           3) Overfeat uses smaller strides thus larger feature maps and better accuracy.

### Feature Extractor : 

There are two models available a fast and an accurate one, the difference is
trivial, architecturally being the parameter size.

### Multi-Scale Classification : 

 - The Alexnet's subsampling method i.e. 4 corners and 1 from center although boosts performance by multi-voting feature but can ignore many regions and is computationally redundant when the views overlap.

- Also it only applies to a single scale which may not be the optimal scale for the object to be recognized with a good confidence.

- They on the other hand explored the entire image by densely running the network at each location and at multiple scales.
- This approach produces more views for multi-voting while still remaining robust and efficient.
- However the subsampling ratio is only 36 when applied densely, i.e. this net will only produce an output every 36 pixels, this is very coarse and the object may not properly  properly align with the sampling window which will give a poor confidence score.
- To circumvent this they apply the "fragmenting" approach from the Fast scanning paper.
- The fully connected classifying layers are sled over the outputs of this maxpooled fragments and outputs a C-dimensional vector(C for classes).
- The final output is a 3D tensor of these multiple classes.(2-spatial dimensions x C-dimensional vectors.)
- The same is repeated over for the same image at multiple scales and horizontal flipping.
- The mean of all these C-dimensional vectors are taken to predict final top-1 and top-5 classes.


Note :  At test time the net can be easily scaled to accomodate any size of image as the convolution operations will simply slide over a bigger image while at the test time the fully connected layers will be replaced by convolution operations with kernels of 1x1 spatial extent with mere thresholding operations.

## Localization: 

For localization the classification layers are replaced by the regression layer and trained to predict bounding boxes at each spatial location and scale, regression predictions are then combined together to produce one bounding box per object with a very strong confidence. 

The classifier and regressor network are both run at the same time at same computation cost minus the final regressor layer's. Each bounding box prediction can be assigned a confidence using corresponding c-vector softmax classification.

The regressor's hidden FCs are 2 in number with 4096 and 1024 channels respectively. Similar to classfication it has (3x3) copies due to fragmentation segmenting

The bounding box merge is greedy, it merges recursively until it's match_score(sum of distance between their centre and intersection area between two boxes) crosses a threshold "t". Multiple low confidence bouding boxes are merged into one single high confidence bounding box, this removes the false positives in the intermediate steps as there are not many boxes of false positives.

## Detection :

Detection is similar to the classification except the background class, to introduce the background class, traditionally random negative examples are taken for training and then the successive passes are run with the most offending negative errors as a bootstrapping passes and again for fine tuning in the further passes making the task complicated, Overfeat does the same but on the fly, since the feature extraction is already trained due to other tasks, they don't need additional fine-tuning they simply select a few random or offending negative examples per image to train the model on which makes it more computationally expensive but renders task more simpler.


## Conclusion :

The Overfeat successfully shows that simultaneously training the same network to do the different tasks improves the efficiency and accuracy of the network on all the networks and gets multiple tasks done at the computational cost of one.
Also combining their approach with the novel fragmentation approach(which already showed excellent results) was a smart move which led them win 2/3 tasks of ILSVRC13 while they stood 3rd on third tasks.

They discuss the future possible improvements such as using IoU loss over L2 loss and backpropping through the whole network during localization.