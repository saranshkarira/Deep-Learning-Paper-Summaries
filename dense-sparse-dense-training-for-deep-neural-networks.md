# DSD: Dense-Sparse-Dense training for deep neural networks
Song Han, Huizi Mao, Enhao Gong, Shijian Tang, William J. Dally, arxiv 2017

## Summary
Authors present a training regime built over their previous paper on network pruning, the regime, as the authors claim, increase the representational power of a DNN. The results on image captioning were quite convincing as well.

Key Contibutions:

- One cycle of this training regime consists of three phases, Dense, Sparse and Dense respectively(D-S-D).
- Initially, the network is fully trained, upto very near to convergence, this is called Dense step.
- The network weights below a certain threshold are replaced with zero.
- The network is then fine tuned for few epochs while freezing/masking the pruned out weights, this is called Dense step.
- The weights are now unfreezed/unmasked and re-run for some epochs, this is called Dense step.
- The cycle is repeated over and over to further improve the results(D-S-D-S-D..).

## Strengths:
- More information can be represented without increasing the model size and thus memory.
- This dense representation is hence reponsible for better predictions.

## Weaknesses/Notes:
- The number of epochs needed per step gives a whole combination of hyperparameters.
