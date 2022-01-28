---
layout: single
title: "Batch Normalization"
categories: ["deeplearning"]
tag: [deeplearning, batch-normalization]
---

Deep Neural Networks might face a variety of problems, for example, gradient vanishing/exploding. As the network gets deeper and deeper, it becomes harder to train on.

Bad initializations such as setting all weights to 0, small values, or large values bring about detrimental impacts on gradients.

There's a number of great and reasonable initialization methods such as Xavier Initialization [paper link](https://proceedings.mlr.press/v9/glorot10a/glorot10a.pdf).

## Batch Normalization

Intuition: Why don't we just "force" each linear activations to have a **unit gaussian distribution**?

This is the key point of batch normalization. If we apply **zero-centering** and **normalization** to each layer's activations, then all the layers' activation units will be unit gaussian activations with **zero-mean** and **standard deviation of 1**.

## Zero-centering and Normalization

Let $x^{(k)}$ be the activation vector of the given layer. Then, we can achieve the above by,
\[ \hat{x}^{(k)}=\frac{x^{(k)} - E[x]}{\sqrt{Var(x)}} \]

## Where to apply?

Batch normalization is usually inserted

**After** FC layers or Conv layers and

**Before** nonlinearity/activation functions.

So the general flow is **FC/Conv -> BN -> Activation**

## Problems

Great! Now we've learned how to normalize the activation layer. But there's one thing we can go deeper about. This normalization definitely prevents saturation, for example, for **tanh** by squashing the activation units around to zero.

However, do we **always** want this saturation? The answer is maybe or maybe not.

So, why don't we let our almighty neural network to handle with that by giving flexibility?

This sounds like a reasonable strategy. The way to achieve this flexibility is to introduce **learnable parameters** that can control the values of $\hat{x}^{(k)}$.

\[ y^{(k)} = \gamma^{(k)}\hat{x}^{(k)}+\beta^{(k)} \]

By setting learnable parameters, we can let the network to decide **how much** it will scale and shift the normalized values $\hat{x^{(k)}}$.

One cool thing is if our almighty network decides that it's the best **NOT** to make the layer activations to unit gaussian, then it can simply recover by setting,

\[ \gamma^{(k)} = \sqrt{Var[x^{(k)}]} \\\ \beta^{(k)} = E{[x^{(k)}]} \]

This computation **recovers** the **identity mapping**. You can put these values into the $\hat{x^{(k)}}$ equation above to check this out.

## Advantages

1. BN allows higher learning rates
2. Reduces the strong dependence on weight initialization since the neural network will find the optimal activation units
3. BN actually performs **regularization**. I first didn't understand why this happens but one you think about the word **batch**, it actually makes sense. BN is performed over the **whole** batch os it introduces gentle generalization effects.

## Conclusion

So far, we've looked at how batch normalization works and why we use it. For further reading, reference the [Loffe, Szegedy., 2015](https://arxiv.org/pdf/1502.03167.pdf)
