# Mathematics

All current ML systems use tensors as their basic data structure.

Models don't process an entire dataset at once. They break the data into small batches.

All transformations learned by models can be reduced to a handful of tensor operations applied to tensors of numeric data:

```python
# Dense layer
output = np.maximum(0, np.dot(W, input) + b)
```

```
                   Input X
                      +
                      |
                      v
               +------|-------+
               |              |
               |    Model     |
               |              |
               +------|-------+
 +---------+   ^      |
 | weights +---+      v
 +-----|---+   >------|------+         +------------+
       ^        |Predictions |         |True Targets|
       |        |     Y'     |         |     Y      |
       |        +-----|------+         +------|-----+
weight |              |                       |
update |              |                       |
       |              |                       |
       |              |     +------------+    |
       |              |     |   loss     |    |
  +----|------+       +---->+   function +<---+
  | optimizer |             +-----|------+
  +----|------+                   |
       ^                          v
       |                     +----|-----+
       +---------------------+loss score|
                             +----------+
```

Loss functions and optimizers are the keys to configuring the learning process. Use binary crossentropy for a two-class classification problem, categorical crossentropy for a many-class classification problem, mean-squared error for a regression problem, connectionist temporal classification (CTC) for a sequence-learning problem.

The typical workflow is

1. define the training data: input tensors and target tensors;

2. define a network of layers (or model) that maps the input to the targets;

3. configure the learning process by choosing a loss function, an optimizer and some metrics to monitor;

4. iterate on your training data by calling the `fit()` method of your model.

There are two ways to define a model: 

1. using the `Sequential` class;

2. the functional API (for directed acyclic graphs of layers), which builds completely arbitrary architectures.
