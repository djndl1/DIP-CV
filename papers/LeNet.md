[1] Y. LeCun et al., “Backpropagation Applied to Handwritten Zip Code Recognition,” Neural Comput., 1989.

[2] Y. LeCun, L. Bottou, Y. Bengio, and P. Haffner, “Gradient-based learning applied to document recognition,” Proc. IEEE, 1998.

# Background

Multiplayer Neural Networks trained with the backpropagation algorithm constitute the best example of a successful Gradient-Based Learning technique. It can be usedc to synthesize a complex decision surface that can classify high-dimension patterns such as handwritten characters with minimal preprocessing.

The variability and richness of natural data make it almost impossible to build an accurate recognition system entirely by hand. Most pattern recognition systems are built using a combination of automatic learning techniques and hand-crafted algorithms, consisting of 

- _feature extractor_: transforming the input patterns so that they can be represented by low-dimensional vectors or short strings of symbols can be easily matched or compared and are relatively invariant w.r.t. transformations and distortions of the input patterns that do not change their nature; It contains most of the prior knowledge and specific to the task, often entirely hand-crafted.

- _classifier_: general-purpose and trainable; 

One problem with the approach is that the recognition accuracy is largely determined by the ability of the designer to come up with an appropriate set of features.

Faster machines, larger real data and the availability of powerful learning techniques has changed the situation that feature extractors were the center of pattern recognition research.

## Learning Machine Model

$$
Y^{p}=F\left(Z^{p},W\right)
$$

- $Z_{p}$: $p$-th input pattern;

- $W$: the collection of adjustable parameters in the system

- $Y^{p}$: may be interpreted as the recoginized class label or as scores or probililities associated with each class

A loss function

$$
E^{p}=D\left(D^{p},F\left(W,Z^{p}\right)\right)
$$

measures the dicrepancy between the correct or desired output $D^{p}$ for pattern $Z^{p}$ and the output produced by the system.

$E_{train}(W)$ is the average of the errors $E^{p}$ over a training set.

The performance is estimated by measuring the accuracy on a set of samples (_test set_) disjoint with the training set. The gap between the expected error rate on the test set $E_{test}$ and the error rate on the training set $E_{train}$ decreases with the number of training samples approximately as 

$$
E_{\text{test}}-E_{\text{train}}=k\left(h/P\right)^{\alpha}
$$

- $P$: the number of training samples;

- $h$: a measure of effective capacity or complexity of the machine;

- $k$: constant

- $\alpha \in [0.5, 1.0]$

There is a trade-off between the decrease of $E_{train}$ and the increase of the gap. Most learning algorithms employ _structural risk minimization_, which attempts to minimize $E_{train}$ as well as some estimate of the gap, implemented by minimizing 

$$
E_{\text{train}}+\beta H\left(W\right)
$$

where $H(W)$ is called a _regularization_ function and $\beta$ is a constant. 

$H(W)$ is chosen such that it takes large values on parameters that belong to high-capacity subsets of the parameter space. Minimizing $H(W)$ in effect limits the capacity of the accessible subset of the parameter space, thereby controlling the trade-off between minimizing the training error and minimizing the expected gap between the training error and test error.

### Gradient-Based Learning

The general problem of minimizing a function w.r.t. a set of parameters is at the root of many issues in CS. In Gradient-based learning, the loss function can be minimized by estimating the impact of small variations of the parameter values on the loss function, measured by the gradient of the loss function w.r.t. the parameters. 

the simplest miminization procedure is the _gradient descent algorithm_ where $W$ is iteratively adjusted as:

$$
W_{k}=W_{k-1}-\epsilon\frac{\partial E\left(W\right)}{\partial W}
$$

where $\epsilon$ is a scalar (constant or variable if necessary). The usefulness of the second-order methods, such as Newton, Quasi-Newton, Conjugate Gradient, to large learning machines is very limited.

A popular one is the _stochastic gradient algorithm. It consists in updating the parameters vector using a noisy, or approximated version of the average gradient:

$$
W_{k}=W_{k-1}-\epsilon\frac{\partial E^{p_{k}}\left(W\right)}{\partial W}
$$

SGD usually converges considerably faster than regular gradient descent and second order methods on large training sets with redundant smaples.

# Ideas

Better pattern recognition systems can be built by relying more on automatic learning, and less on hand-designed heuristics. Hand-crafted feature extraction can be advantageously replace4d by carefully designed learning machines that operate directly on pixel images. 



