#Deep Compression: Compressing Deep Neural Networks with Pruning, Trained Quantization and Huffman Coding
Song Han, Huizi Mao, William J. Dally, ICLR, 2016

##Summary
The conventional neural networks tend to be both computationally as well as memory intensive, The authors propose "Deep Compression" a three stage pipeline: Pruning, Trained Quantization and Huffman coding.
Altogether, they reduce the parameter storage by 35x to 49x without hurting accuracy. This has a lot of practical use-cases, from deploying on embedded system to loading the whole network into on-chip SRAM cache. For example, the 240MB Alexnet reduces to mere 6.9MB, 552MB VGG-16 reduces to 11.3MB. A speed up of 3x to 4x and energy efficiency of 3x to 7x is also recorded.

Key contributions:

-Pruning : The principle assumption behind pruning is that a lot of weights after training are near to zero and thus contribute negligibly to the final prediction, pruning simply takes a threshold parameter(0.3) and puts all the weight values below it to zero. After the pruning the network is retrained for a few epochs for fine tuning. Although the pruning reduces the network's parameters by 9x-13x, the computing is still going to be wasted due to zero multiplication in the sparse matrix, Thus the sparse matrix is represented in a general CSC format(Compressed Sparse Column). Further, in the CSC format, they store the positions of the non-zero elements are saved as the distance from the previous such element rather than absolute position, and thus are able to encode this difference in 8 and 5 bits for conv and fc layer respectively, when and if the difference exceeds this bit bound, the value of the zero at the bound is also stored as a filler zero.
-Quantization (and weight sharing) : K-means clustering is used to cluster the weights into "bins", the weights are then indexed and the centroids of each cluster is taken as the common shared weight of all the eliments of the cluster and during training/fine tuning, each element contributes in the centroid's weight update.
--The initialization of the centroids hugely impact the quality of clustering and for such three alternatives are analyzed and 'Linear initialization' is proposed as the best among them for this method.
-Huffman coding : The distribution of the weights after quantization is analyzed using by making a histogram out of these bins, i.e. how many elements each cluster/bin has, the weights are then encoded using lossless Huffman representation(most recurring centroids are represented by smaller bits and vice versa)

##Strengths 
-Improved speedups, energy efficiency
-Reduced Parameter Storage
-No loss in accuracy
-One of the most interesting and refreshing papers I've come across

##Weakness/Notes
-This is only a test/usage time speed up, the train time and memory build up are still the same.
-The method, especially pruning is a cure to the redundant weight buildup during training, we'd like a preventation of this build up, though this is the necessary first step.
-The method is analytical and manual, we need to analyse a lot at each stage to determine the hyperparameters(of dropping weights, centroid initialization, Huffman encoding). We'd be more interested to give this as a flexible dimension to our net to explore.

