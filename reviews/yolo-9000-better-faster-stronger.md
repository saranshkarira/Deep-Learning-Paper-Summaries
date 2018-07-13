# YOLO9000: Better, Faster, Stronger
Joseph Redmon, Ali Farhadi

## Summary
YOLO9000 is a state-of-the-art real time object detector that can detect over 9000 categories, which is achieved by a joint training over COCO detection dataset as well as Imagenet Classification Dataset.
The model is an improvisation over YOLO to overcome its limitations and achieves 78.6 mAP at 40 FPS, though FPS can be increased at a cost of lower mAP.

Key Contributions:

- Authors argue that the detection datasets are not as rich in vocabulary as their classification counterparts, they propose a method to harness the classification data in the detectors.

- Better : 
    - The error analysis of orignal YOLO shows that the system is makes a significant number of localization errors as well as has a poor recall as compared to its ROI counterparts.

    - Batch Normalization on all conv layers improves convergence while eliminates need of dropout and other regularizing methods. Also gives a 2% boost to mAP.

    - Yolo used to train classifier on low res and switched to high res during detection, to reduce this load of learning high res as well as detection simultaneously author fine tune the classifier on high res for 10 epochs before transfering. Gives a 4% mAP boost.

    - Authors use anchor boxes to make learning easier, also it improves recall, authors found k-means clustering a better approach than hand-picked priors.

    - Anchor boxes are constrained to grid cells, such constraints results in model stability.

    - Fine grained features are necessary for small object detection, for this authors concatenate features from a layer before which is at 26x26 and instead of pooling, they reorg each 26x26 map into four 13x13 maps.

    - Multi-Scale training for learning features at different scales.

- Faster :
    - Darknet-19, a new feature extractor based on the principles of VGG(3x3 conv and doubling the no of channel after each pooling) along with 1x1 conv and Batch Normalization per layer to compress representation while speeding up convergence and regularizing the model.

- Stronger :
    - Authors jointly train the detector on both COCO as well as Imagenet classification data, during classification, only classification loss being backpropogating only to classification specific parts.
    - Since, softmax is mutually exclusive, the classes of both the datasets that are correlated such as 'dog' and 'terrier' pose a problem, thus they use a multi-label model that does not assume mutual exclusion.
    - Authors pull Imagenet labels from yet another database called wordnet(which is a directed graph) to hierarchially arrange the classes, example- Dogs > Terriers > Norfolk terrier.

## Strengths 

- Can detect more than 9000 classes.
- Real-time detection speeds.
- Beats Faster-RCNN and SSD at 40 FPS

## Weakness:

- Not state-of-the-art accurate at high speeds.
- It could've used faster feature extractors such as ResNets or DenseNets instead of VGG-style nets.
- Still poor at detecting small objects.
- Wrong analogy with Resnet for reorg, resnet sums not concat.