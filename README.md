# Semantic Segmentation of Remote Sensing Images  
## U-Net vs. SAM (Segment Anything Model)

This project compares a classical convolutional neural network (U-Net) with a pre-trained foundation model (SAM) for land cover segmentation on the DeepGlobe dataset.

The goal is to analyze the effectiveness of transfer learning in remote sensing tasks and evaluate architectural trade-offs between task-specific CNNs and large-scale pre-trained models.

---

## Dataset

We use the **DeepGlobe Land Cover Classification Dataset**, which contains:

- High-resolution RGB satellite images
- Pixel-wise annotated segmentation masks
- Multiple land cover classes (urban, agriculture, forest, water, etc.)

The dataset is split into:

- 70% Training
- 15% Validation
- 15% Test

---

## Models

### 1. U-Net (Baseline)
- Encoder-decoder CNN
- Skip connections
- Fully trainable end-to-end

### 2. SAM-based Model
- Pre-trained SAM vision encoder (frozen)
- Custom CNN segmentation head:
  - 3×3 Conv → BN → ReLU  
  - 3×3 Conv → BN → ReLU  
  - Bilinear upsampling  
  - 1×1 Conv (class prediction)

---

## Training

- Loss: Cross-Entropy (optional weighted / Focal Loss)
- Optimizer: AdamW
- Learning rate scheduler: ReduceLROnPlateau
- Early stopping based on validation mIoU
- Logging via CSV and TensorBoard

---

## Evaluation

Models are evaluated using:

- Pixel Accuracy
- Mean Intersection over Union (mIoU)
- Per-class IoU
- Confusion Matrix (raw and normalized)

Qualitative results include visualization with dynamic class legends.
