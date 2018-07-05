# Some Improvements on Deep Convolutional Neural Network based Image Classification
Andrew G. Howard

# Summary
The paper focuses on purely Image augmentation techniques to improve the accuracy of the network, using their strategies they were able to improve on the previous year's winner Alexnet by about 3.5% on top-5 error rate @13.55%

Key Contributions:
- They doubled the size of fully convolutional layer without any significant improvements.
- The Alexnet took random crops after rescaling an image from smaller side and then cropping the bigger side, they maintained the aspect ratio and pulled random crops out of the whole image.
- They randomly manipulate image's contrast, brightness and color within limits and then add random lightning similar to Alexnet.
- At test time addition to 5 translations, 2 random flips they also perform predictions at 3 scales and 3 crops.
- This increases the total predictions to 90 this increases the inference time by 10x which they reduce by greedily selecting top 10 augmentations with negligible reduction in accuracy.
- They were also the first ones to implement transfer learning, to train higher resolution models, they used pretrained models on smaller resolution for better initialization and trained the model in 30 epochs which would usually take 90 epochs from scratch.
In higher resolution models, instead of 5 crops they took 9 crops and applied the greedy algorithm.

## Strengths
-Shows feeding the same data to the same network but in creative ways can reduce the error rate so much all on it's own.
## Weakness
- Authors applied all the techniques altogether haphazardly, which unfortunately doesn't tell the contribution of these techniques on individual level.
- On increasing resolution, the reason to keep smaller scale image's crop mutually exclusive doesn't have any proper intuition or logical explanation.
- They didn't try to even improve on the hyper-parameters of the network, they might have won the competition if they even did so in trial and error fashion