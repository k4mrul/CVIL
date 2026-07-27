
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

### Adam
Adam is an optimizer that combines momentum with an adaptive learning rate. It gives each parameter its own learning rate based on its previous gradients.

For example, parameters that change frequently may receive smaller updates, while parameters that rarely change may receive larger updates. Adam is often a good starting optimizer.

### AdamW
AdamW is a modified version of Adam that applies weight decay separately from the gradient update. In standard Adam, weight decay is applied to the gradient before the adaptive scaling, which causes the regularization strength to interact poorly with the adaptive learning rates.

In AdamW, weight decay is applied directly to the weights after the adaptive step. This usually handles regularization (helps prevent a model from overfitting by discouraging it from memorizing the training data) more correctly than standard Adam and can improve how well a model performs on unseen data.

### Weight Decay
Weight decay discourages the model from having excessively large weights. It gradually pushes weights toward zero and helps prevent overfitting.

For example, if a model memorizes its training examples, weight decay can encourage it to learn simpler and more general patterns.

### Learning Rate Schedules
A learning rate schedule changes the learning rate during training.

Usually, training begins with a relatively large learning rate for fast progress. Later, the learning rate becomes smaller so the model can make careful adjustments near a good solution.

### Cosine Annealing
Cosine annealing gradually decreases the learning rate following a smooth cosine-shaped curve.

For example, the learning rate may start at 0.01, decrease slowly at first, fall more quickly in the middle, and approach 0.0001 near the end of training.

### Warmup
Warmup starts training with a very small learning rate and gradually increases it to the desired value.

For example, the learning rate might increase from 0.00001 to 0.001 during the first 1,000 steps. This prevents large, unstable updates at the beginning of training.

### Vanishing Gradients
Vanishing gradients happen when gradients (gradient tells the model how each weight affects the loss) become extremely small while moving backward through a deep neural network.

As a result, the earlier layers receive almost no updates and learn very slowly. This commonly occurs with deep networks using sigmoid or tanh activation functions.

### Exploding Gradients
Exploding gradients happen when gradients become extremely large during backpropagation (helps the model learn by adjusting its weights based on its mistakes).

This can cause huge weight updates, unstable training, or NaN loss values. Gradient clipping is commonly used to limit the size of gradients.

### Backpropagation and the Chain Rule
Backpropagation calculates how much each weight contributed to the model’s error. It starts from the output layer and moves backward through the network.

Backpropagation uses the chain rule to calculate how connected operations affect one another. For example: Imagine the data flows like this:

Weight → Hidden Layer → Output → Loss

Backpropagation starts at the loss and moves backward through the network. At each layer, it calculates how much that layer contributed to the error using the chain rule. These gradients are then used to update the weights and improve future predictions.
