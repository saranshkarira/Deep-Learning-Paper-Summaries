# YOLOv3: An Incremental Improvement
Joseph Redmon, Ali Farhadi

## Summary
YOLOv3 is a minor improvement upon it's predecessor, @28.2 mAP it is as accurate as SSD while 3x faster.

Key Contributions:

- It predicts objectness score per bounding box using logistic regression, which is one for the prediction that overlaps the most, hence True Positive while ignoring others.

- MultiLabel classification is used same as V2 but since softmax is mutually exclusive, it's more efficient to use binary cross-entropy loss using multiple logistic units.

- Predicts over 3 scales, for each scale, taking feature maps from earlier layers but instead of downsampling previous features, V3 upsamples the current features to fit the dimension for element-wise addition as in ResNets.

- 9 different K-means cluster priors are used divided equally among 3 scales.

- Feature extractor is same as Darknet-19 except residual connections and is 53 layers deep.

## Strengths

- The classifier DarkNet-53, beats ResNet-101 and equally matches ResNet-152 in top-5.
- Achieves highest measured FLOP rate, meaning network utilizes GPU better, making it efficient and faster.

## Weakness

- Poor performance in large object detections.

- Carelessly written, feature maps used for different scales not clarified.

- No more Real-Time detection.