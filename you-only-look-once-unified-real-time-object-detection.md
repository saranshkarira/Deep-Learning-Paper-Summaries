# You Only Look Once: Unified, Real-Time Object Detection
Joseph Redmon, Santosh Divvala, Ross Girshick, Ali Farhadi, arxiv, 2015

## Summary 
The authors present a refresing perspective to tackle the object detection problem. Unlike it's predecessors, YOLO framework performs detection in a much simpler single pass making it fast enough for real time Object Detection

Key Contributions:

- While previous frameworks optimized their network for classification problem and run it through hundreds of bounding box proposals in a single image to perform detection, YOLO framework is a simple and efficient single end-to-end pipeline that looks at the whole image at once to perform both detection as well as classification.
- The image is divided into 7x7 grid, each grid is responsible to predict 2 bounding boxed and give exactly one classification.
- The grid cell on which the center of the object falls is responsible to predict that box.

## Strengths

- Fast : The base network runs at 45fps while there's even a faster version running at more than 150 fps.
- Fewer background mistakes : YOLO gets the global context of the whole image making it less error prone to detect background as object.
- Generalized : YOLO learns highly generalizable representations of objects, it significantly outperforms tops detection methods when trained on natural images but tested on artwork.

## Weakness/Notes

- More localization errors.
- mAP is not state of the art at 57.9% compared to 70.4% of Faster RCNN.
- At most only one object can be detected per grid cell and thus easily misses small objects.