# Automated Dental Age Estimation Using YOLOv8 and EfficientNet

## Overview

This repository presents an automated dental age estimation system based on a **two-stage deep learning architecture**. The framework integrates **YOLOv8** for tooth detection and Region of Interest (ROI) extraction from panoramic dental X-ray images, followed by **EfficientNet** for **chronological age regression**.

The proposed method is designed to reduce subjectivity, inter-observer variability, and processing time associated with traditional manual dental age assessment, making it suitable for **forensic odontology** and **clinical dentistry** applications.

---

## Methodology

The system operates sequentially in two stages:

### Stage 1: Tooth Detection (YOLOv8)

* Detects individual teeth from panoramic X-ray images
* Generates bounding boxes and crops tooth ROIs

### Stage 2: Age Estimation (EfficientNet)

* Uses ImageNet-pretrained EfficientNetB0
* Performs regression to predict chronological age
* Trained using a **three-phase progressive fine-tuning strategy**

---

## Training Strategy

EfficientNet is trained using the following staged approach:

| Phase | Description                                | Learning Rate | Epochs |
| ----- | ------------------------------------------ | ------------- | ------ |
| 1     | Regression head training (backbone frozen) | 1e-3          | 50     |
| 2     | Partial fine-tuning (top layers unfrozen)  | 1e-4          | 50     |
| 3     | Full fine-tuning (all layers unfrozen)     | 1e-5          | 100    |

Regularization techniques include **Dropout** and **Early Stopping** to prevent overfitting.

---

## Dataset

Two public datasets are used:

1. **UFBA-UESC Dental Images**

   * Used for YOLOv8 tooth detection training

2. **Zenodo: Panoramic Dental X-rays for Age Estimation**

   * Subjects aged 9–19 years
   * Used for age regression

Datasets are **not included** in this repository and must be downloaded separately due to licensing restrictions.

---

## Experimental Setup

* Framework: TensorFlow / Keras
* Hardware: NVIDIA GPU (Tesla T4 recommended)
* Input size: 224 × 224 pixels
* Optimizer: Adam
* Loss function: Mean Squared Error (MSE)
* Evaluation metric: Mean Absolute Error (MAE)

---

## Results

* **Validation MAE:** 1.97 years
* Age range: 9–19 years
* Demonstrates good generalization with minimal overfitting

The results indicate that isolating teeth using YOLOv8 before regression significantly improves age estimation accuracy.

---

## Repository Structure

```
Deep_Learning.ipynb # Main notebook for training and experimentation
content/
├── dental_data/ # Raw panoramic X-ray images
├── yolo_dataset/ # YOLOv8 formatted dataset (images + labels)
├── tooth_crops/ # Cropped tooth ROIs from YOLOv8
├── models/ # Trained YOLOv8 and EfficientNet models
├── age_labels.csv # Image paths and chronological age labels
└── README.md
```

---

## Applications

* Forensic age estimation
* Pediatric dentistry
* Orthodontic assessment
* Medical image analysis research

---

## Limitations

* Performance depends on tooth detection accuracy
* Domain shift from different X-ray devices may affect generalization
* Demographic and biological variability not explicitly modeled

---

## Future Work

* Larger and more diverse datasets
* Gender-specific age estimation models
* Improved handling of missing or impacted teeth
* Integration with multimodal or 3D dental imaging

---

## Citation

If you use this work, please cite the accompanying paper:

**Automated Dental Age Estimation Based on Panoramic X-Ray Images Using a Hybrid YOLOv8 and EfficientNet Architecture**
Faculty of Computer Science, Universitas Brawijaya

---

## Acknowledgment

We thank Universitas Brawijaya and the creators of the UFBA-UESC and Zenodo dental X-ray datasets for providing the resources necessary for this research.
