# Tumor Morphology Segmentation using U-Net

This repository presents an end-to-end deep learning pipeline for **brain tumor segmentation from MRI images** using a **U-Net architecture**, followed by **morphological analysis** of the segmented tumor regions. The project focuses on both segmentation accuracy and interpretability, aligning with biomedical imaging and computational biology research practices.

---

## Project Overview

Accurate tumor segmentation is a fundamental task in medical image analysis, enabling quantitative assessment of tumor size and shape. In this project, we:

- Train a U-Net model to segment tumor regions from brain MRI slices
- Evaluate segmentation quality using Dice coefficient and Intersection-over-Union (IoU)
- Extract interpretable morphological features from predicted tumor masks

This pipeline demonstrates how deep learning–based segmentation can support downstream tumor morphology and microenvironment analysis.

---

## Dataset

- **Modality:** Brain MRI  
- **Task:** Binary tumor segmentation  
- **Structure:**
    data/
      -data/
      -images/
      -masks/
  - All images are resized to `128 × 128` and normalized to the range `[0, 1]`.

---

## Model Architecture

- **Model:** U-Net (encoder–decoder with skip connections)
- **Encoder:** Convolution → ReLU → MaxPooling
- **Decoder:** Transposed Convolutions with skip connections
- **Loss Function:** Binary Cross-Entropy
- **Optimizer:** Adam

U-Net is particularly well suited for biomedical image segmentation due to its ability to preserve spatial detail while capturing global context.

---

## Segmentation Performance

The model was evaluated on a held-out validation set.

| Metric | Value |
|------|------|
| Dice Coefficient | **0.71** |
| Intersection-over-Union (IoU) | **0.61** |

These results indicate effective tumor localization despite strong class imbalance, where tumor regions occupy only a small fraction of the image.

---

## Morphological Feature Extraction

Using the predicted segmentation masks, we compute simple and interpretable geometric features:

- **Tumor Area:** Number of pixels classified as tumor
- **Tumor Perimeter:** Length of the tumor boundary
- **Tumor Compactness:**  
\[
\text{Compactness} = \frac{4\pi \times \text{Area}}{\text{Perimeter}^2}
\]

To ensure numerical stability, morphological features are computed **only for slices containing non-trivial tumor regions**.

### Aggregate Morphology Statistics

- **Valid tumor slices:** 566  
- **Mean tumor area:** ~268 pixels  
- **Mean compactness:** **0.88**

The high compactness value indicates coherent and well-defined tumor shapes in the predicted segmentation masks.

---

## Qualitative Results

Predicted masks are visually compared with ground-truth annotations. The model consistently localizes tumor regions, with minor boundary over-segmentation, a common characteristic of recall-oriented segmentation models.

---

## How to Run

1. Clone the repository:
 ```bash
 git clone https://github.com/your-username/tumor-morphology-segmentation.git
 cd tumor-morphology-segmentation

2.Open the Notebook
UNET SEGMENTATION.ipynb
