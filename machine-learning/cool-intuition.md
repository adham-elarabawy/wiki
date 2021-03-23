# Cool Intuition

While developing my understanding of machine learning, I found the following points to be intellectually stimulating and interesting. 

### Why do artificial neurons have continuous activations instead of being active/inactive in a binary way -- the way that biological neurons are?

The heart of training neural networks is just minimizing some cost/loss function. The methods used to minimize the loss function \([Backpropagation](neural-networks/backward-propagation.md), [Optimizers](neural-networks/optimizers.md), Gradient Descent\) are rooted in being able to  compute derivatives on our loss function, which means that it must be a relatively nice and smooth function. If the artificial neurons were binarily activated, then the resultant loss function would have many discontinuities.

