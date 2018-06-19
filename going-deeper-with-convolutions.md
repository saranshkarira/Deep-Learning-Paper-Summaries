# Going Deeper with Convolutions
Christian Szegedy, Wei Liu, Yangqing Jia, Pierre Sermanet, Scott Reed, Dragomir Anguelov, Dumitru Erhan, Vincent Vanhoucke, Andrew Rabinovich, ArXiv'14

## Summary
This paper is practical implementation of Arora's paper on theoretical explanation for success of deep nets, authors propose some improvements based on the suggestions of the paper, the collective of which is called Inception Architecture, an instance of which, called GoogLeNet went on to win ILSVRC'14.

Key Contributions:

- The simplest way to improve performance of any neural net is to increase its size.
- However, a bigger model is more complex thus more prone to overfit also more parameters make it resource intensive. This is dramatically reduced by using 1x1 convolution filters to reduce number of filters going in for further 3x3 and 5x5 convolutions.
- Modular approach is used so that a single small module is made with high optimization and stacked on top of one another to make as deep network as needed.
- 3x3 and 5x5 filters are used simultaneously to handle multiple scales.
- Adding a parallel max-pool pipeline seems to improve accuracy.
- To backpropogate gradients back effectively in such a deep network, auxillary classifiers are connected to intermediate layers since intermediate layers seem to be very discriminative this quality is also bought down to lower layers.
    - At train time their is summed with total loss in weighted fashion.
    - At test time they are discarded

## Strengths

- The paper successfully approximates a sparse network into a dense one, improving the richness of feature maps and thus producing excellent results on ILSVRC'14.

## Weakness/Notes

- Though authurs try to explain the intution behind, they still seem unsure whether that is actually the case.
