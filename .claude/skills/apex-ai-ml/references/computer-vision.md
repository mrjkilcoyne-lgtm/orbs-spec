# Computer Vision

## Scope
Processing and interpreting images: classification, object detection, segmentation, pose estimation, and vision transformers. Datasets, augmentation, and evaluation metrics.

## Core principles
- Image classification (identify the object in an image) is the foundation: CNNs learn hierarchical features. Transfer learning from ImageNet pre-training is standard.
- Object detection (find and classify multiple objects) requires localizing bounding boxes. Architectures: RCNN (region-based), YOLO (single-shot), SSD. Speed vs. accuracy tradeoff: YOLO is fast, RCNN is accurate.
- Semantic segmentation (classify each pixel) requires spatial precision. Encoder-decoder (U-Net) or dilated convolutions preserve resolution. Instance segmentation (separate each object) adds another layer of complexity.
- Data augmentation (random crops, flips, color jitter, perspective transforms) is crucial for images; models overfit to training set specifics. Test-time augmentation (ensemble predictions from augmented crops) improves results.
- Evaluation metrics vary by task: accuracy for classification (brittle with class imbalance), mAP (mean average precision) for detection, IoU (intersection over union) for segmentation. Task-specific metrics guide optimization.

## Apex practices
- Use pre-trained CNNs (ResNet, EfficientNet, Vision Transformers) from timm (PyTorch Image Models) or TensorFlow Hub. Fine-tune on your data.
- Implement modern data augmentation (AutoAugment, RandAugment, Mixup) during training; they reduce overfitting and improve accuracy.
- Use detection/segmentation frameworks (Detectron2, MMCV) rather than implementing from scratch. They handle data loading, augmentation, and standard architectures.
- Benchmark on standard datasets (ImageNet, COCO, Pascal VOC) if possible; this enables comparison and reduces chance of local overfitting.

## Pitfalls
- Using inadequate image resolution; if training on 224x224 but deploying on 4K, accuracy degrades. Match training and inference resolutions.
- Not accounting for class imbalance in detection; rare objects are underfitted. Use weighted loss or focal loss (penalizes easy examples less).
- Trusting bounding box predictions without checking calibration; a network outputting high confidence doesn't mean it's right. Measure and calibrate uncertainty.

## Tools & references
PyTorch, torchvision, timm (PyTorch Image Models), Detectron2 (detection/segmentation), "Computer Vision: Algorithms and Applications" (Szeliski), COCO dataset, ImageNet, vision transformer papers (ViT, CLIP).
