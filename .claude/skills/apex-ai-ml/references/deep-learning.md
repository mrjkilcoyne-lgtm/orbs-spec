# Deep Learning

## Scope
Neural networks with multiple layers: backpropagation, activation functions, and training dynamics. Building blocks for computer vision, NLP, and generative models.

## Core principles
- Deep neural networks are universal function approximators: given enough layers and neurons, they can learn any continuous function (in theory). In practice, depth enables learning hierarchical representations (low-level features → concepts → high-level abstractions).
- Backpropagation is the workhorse: compute gradients of the loss with respect to all weights via chain rule, then update weights to reduce loss (gradient descent). No backprop, no deep learning at scale.
- Activation functions (ReLU, tanh, sigmoid) introduce nonlinearity. Without them, stacking linear layers is just one linear layer. ReLU (rectified linear unit, max(0, x)) is default; it's fast and trains well.
- Vanishing gradients plague deep networks: gradients shrink exponentially with depth (gradient = product of local gradients, each <1). Fixes: skip connections (ResNets), layer normalization, better weight initialization (He, Xavier).
- Overfitting is the constant threat: networks with billions of parameters memorize training data. Regularization: L1/L2 weight penalties, dropout (randomly zero activations during training), data augmentation, early stopping.

## Apex practices
- Start with a pre-trained model (transfer learning) on a related task; fine-tuning on your data is cheaper than training from scratch. ImageNet pre-training, language-model pre-training are powerful.
- Use batch normalization (normalize layer inputs to mean 0, std 1) to stabilize training and enable higher learning rates. This is standard.
- Implement learning rate schedules (decay over time, cosine annealing) to improve convergence. Fixed learning rates rarely converge cleanly.
- Visualize gradients: if gradients are dying (zero) or exploding (huge), something's wrong. Gradient clipping (cap gradient norm) is a quick fix; fundamental issues require architecture changes.

## Pitfalls
- Training without validation monitoring; the loss decreases but the model overfits silently. Validation loss plateau is your signal to stop.
- Using inappropriate optimizers (vanilla SGD on modern tasks is slow; use Adam, AdamW). Momentum and adaptive learning rates matter.
- Not initializing weights carefully; random Gaussian initialization (0, 1) is too large for deep networks. Use Xavier/He initialization.

## Tools & references
PyTorch, TensorFlow/Keras, "Deep Learning" (Goodfellow, Bengio, Courville), "Neural Networks from Scratch" (Trask), backpropagation visualizations, optimization surveys (SGD, Adam, AdamW).
