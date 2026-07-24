
### Optimization
Optimization means adjusting a model’s parameters—such as weights and biases—to reduce its error or loss.

For example, if a model predicts a house price as $80,000 when the actual price is $100,000, optimization changes the model’s weights so that its future predictions become closer to the correct price.

### Gradient Descent
Gradient descent is an optimization method that moves model parameters in the direction that decreases the loss.

For example, If a model's loss increases when a particular weight is increased slightly, gradient descent will decrease that weight by a small step proportional to the negative gradient.

### SGD
Stochastic Gradient Descent (SGD) updates the model using one training example, or a small batch, instead of the entire dataset.

For example, rather than checking all 10,000 images before updating the model, SGD may update it after every batch of 32 images. This makes training faster but introduces some randomness.

### Momentum
Momentum helps SGD move faster in a consistent direction and reduces unnecessary back-and-forth movement.

It is similar to a ball rolling downhill. The ball gathers speed while moving in the same direction, making it harder to stop suddenly.
