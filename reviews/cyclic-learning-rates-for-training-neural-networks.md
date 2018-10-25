# Cyclic Learning Rates for Learning Neural Networks
Leslie N. Smith, ARXIV, 2017  

## Summary
Learning rate is the most important hyper-parameter to tune to train a Neural Network. This paper is the first in the line of papers from Leslie that remove the guesswork based experimentation work to find the best learning rate with a disciplined approach.

Key Contribuitions:

- Cylic learning rates : Usually learning rates are kept to a singular value and tuned as the training proceeds either manually or dynamically(computational overkill). Leslie suggests that cycling the learning rates within the bounds of optimum range of learning rates gives better results/test-accuracy.

- LR range test : To find these bounds Leslie suggests to do a LR test, basically run the training for a few epochs and keep increasing learning rate from a very low value, graph these along with their corresponding loss values or even better Accuracy. And pick the optimum learning rate as the lr-max.

- For lr-min take the 1/4 or 1/3 of the lr-max. These are the bounds of the cycle.

- To determine how many iterations each cycle should last, Leslie suggests anything between 2*epoch to 10*epoch will work without much difference if any.

- While doesn't show any much effect when combined with Dynamic LR methods, when combined with nestrov the number of iterations reduce to approx. 1/3 in the shown experiments while giving similar accuracy result.

## Strengths 

- Efficient, only required 10-15 lines of generic code to implement in almost any of my existing code including range test.
- Faster Feedback, if you've ever trained resnets you'll be familiar with elbow curves, the ones that give a constant saturation for a long long time and then drop suddenly, I didn't face any such curve using this scheduler with vanilla SGD.


## Weakness:
- A lot of open ends, the paper leaves a lot of open ended questions even the basic hows and whys. Not actually a weakness but an open to explore area and Leslie actually goes ahead to answer and improve them in subsequent papers.
