# Convolutional Neural Networks

## Scope
CNNs for image processing: convolutional and pooling layers, feature hierarchies, and inductive biases for spatial data.

## Core principles
- Convolutional layers exploit spatial structure: a small kernel (filter) slides across the image, capturing local patterns (edges, textures). Sharing weights across positions (convolution) reduces parameters vs. fully connected layers.
- Each layer builds on the previous: early layers learn low-level features (edges, corners), middle layers combine them (textures, shapes), deep layers recognize objects (faces, dogs). This hierarchy is the key insight.
- Pooling (max or average over small windows) reduces spatial dimensions, discards fine details, and helps the network learn invariant representations (object recognizable at different scales/positions).
- Receptive field (the region of input each neuron sees) grows with depth. Deep networks have large receptive fields, able to integrate global context; shallow networks are local.
- Transfer learning is powerful: ImageNet pre-trained CNNs (ResNet, VGG, EfficientNet) transfer to new tasks (medical imaging, satellite imagery) with fine-tuning. Pre-trained features are often better than training from scratch on small datasets.

## Apex practices
- Use pre-trained models from torchvision or TensorFlow Hub; training from scratch is expensive (GPUs, data). Fine-tune the last layers on your domain data.
- Implement data augmentation (random crops, rotations, color jitter) during training to reduce overfitting and improve robustness. Test-time: use center crop or ensemble predictions.
- Monitor GPU memory and use gradient checkpointing if the model doesn't fit; checkpointing trades memory for computation (recompute activations during backprop).
- Visualize learned filters (early layers show edge detectors, deep layers show object parts) to understand what the network learned. Tools: activation maximization, saliency maps.

## Pitfalls
- Not applying data augmentation; CNNs overfit to training image statistics (exact positions, lighting). Augmentation is crucial.
- Assuming a larger model is always better; EfficientNet scales optimally (depth, width, resolution together); a naive deep ResNet may be slower.
- Forgetting normalization (subtract ImageNet mean, divide by std) during inference; pre-trained models expect this preprocessing.

## Tools & references
PyTorch torchvision, TensorFlow/Keras, ResNet/VGG/EfficientNet architectures, "Visualizing and Understanding Convolutional Networks" (Zeiler & Fergus), grad-CAM for interpretability.
