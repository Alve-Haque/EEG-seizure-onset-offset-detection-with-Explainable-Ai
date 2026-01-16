# 🧠 EEG Signal Onset-Offset Detection With Explainable Ai

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Key Contributions](#-key-contributions)
- [Dataset Description](#-dataset-description)
- [Signal Preprocessing](#-signal-preprocessing)
- [Data Pipeline](#-data-pipeline)
- [Method 1: Feature-Based Signal Processing Model](#-method-1-feature-based-signal-processing-model)
- [Method 2: CNN + BiLSTM + Attention (Deep Learning)](#-method-2-cnn--bilstm--attention-deep-learning)
- [Explainable AI (XAI) Techniques](#-explainable-ai-xai-techniques)
- [Results Summary](#-results-summary)
- [Future Improvements](#-future-improvements)
- [Business Value](#-business-value)
- [Citation](#-citation)
- [Acknowledgments](#-acknowledgments)

---


## 📌 Overview

Epileptic seizure detection from Electroencephalography (EEG) signals is a critical task in clinical neuroscience. Manual EEG interpretation is time-consuming, subjective, and prone to error due to the complex temporal dynamics of brain activity.

This project presents a **comparative, data-driven framework** for automated seizure detection and seizure onset–offset localization using EEG signals. Two complementary approaches are explored:

1. **Classical signal processing with handcrafted features**
2. **A deep learning architecture combining CNN, BiLSTM, and Attention**

To ensure **clinical transparency and trust**, we integrate **Explainable Artificial Intelligence (XAI)** techniques that visually highlight which EEG regions influence the model’s decisions.

---
## 💼 Business Value

This project delivers tangible value across **clinical, research, and commercial domains** by combining high-performance seizure detection with interpretability.

### Clinical Impact
- Enables **early and accurate seizure detection**, improving patient safety
- Provides **transparent decision support** through XAI, increasing clinician trust
- Supports seizure **onset–offset localization**, aiding treatment planning

### Research & Innovation Value
- Serves as a **benchmark framework** for EEG-based seizure analysis
- Demonstrates how attention mechanisms enhance both **performance and interpretability**
- Easily extensible for patient-specific and real-time systems

### Operational & Commercial Value
- Reduces reliance on manual EEG review, lowering **operational costs**
- Scalable architecture suitable for **hospital monitoring systems**
- Strong foundation for **medical AI products**, clinical tools, and regulatory pathways

By bridging accuracy, interpretability, and scalability, this system is well-positioned for real-world deployment in healthcare environments.

## ✨ Key Contributions

- Dual-method comparison: feature-based vs deep learning
- Accurate **seizure classification** and **onset–offset regression**
- Robust handling of **heterogeneous EEG data**
- Attention-based **Explainable AI** visualizations
- Clinically interpretable and scalable design

---

## 📊 Dataset Description

- **Total EEG recordings:** 6,190  
  - Seizure: 2,421  
  - Non-seizure: 3,769
- **Channels:** 19 original EEG channels (reduced to 6)
- **Sampling frequencies:** 250, 256, 400, 500, 1000 Hz
- **Signal duration:** Up to 60 minutes
- **Annotations:** Seizure onset and offset timestamps

---

## 🔧 Signal Preprocessing

EEG signals exhibit noise, variable sampling rates, and inconsistent lengths. A standardized preprocessing pipeline is applied to ensure robustness.

### 1. Noise Removal
- **50 Hz IIR Notch Filter**  
  Removes power-line interference while preserving neural activity.

### 2. Bandpass Filtering
- **FIR Bandpass Filter (0.5–70 Hz)**  
  Retains clinically relevant EEG bands:
  - Delta
  - Theta
  - Alpha
  - Beta
  - Gamma

### 3. Resampling
- All signals are resampled to **250 Hz** to ensure uniform temporal resolution.

### 4. Channel Selection
- From 19 channels, **6 representative channels** are selected to:
  - Reduce redundancy
  - Lower computational cost
  - Preserve seizure-relevant activity

### 5. Segmentation
- Sliding window segmentation is used
- Short signals are padded to maintain consistency

---

## 🔄 Data Pipeline

```
Raw EEG Signals
      ↓
Notch Filtering (50 Hz)
      ↓
Bandpass Filtering (0.5–70 Hz)
      ↓
Resampling (250 Hz)
      ↓
Channel Selection (6 Channels)
      ↓
Segmentation (Sliding Windows)
      ↓
Model Input
```

Two parallel pipelines are used depending on the method:

- **Method 1:** Feature extraction → Fully connected model  
- **Method 2:** Raw signal → CNN–BiLSTM–Attention model

---

## 🧪 Method 1: Feature-Based Signal Processing Model

### Feature Extraction

For each of the 6 EEG channels:

#### Frequency-Domain Features
- Delta band power
- Theta band power
- Alpha band power
- Beta band power
- Gamma band power

#### Time-Domain Statistical Features
- Mean
- Standard deviation
- Root Mean Square (RMS)
- Skewness
- Kurtosis

➡ **Total features:** 60 per EEG segment

---

### Model Architecture

- Fully connected layers:  
  `60 → 256 → 128 → 64`
- ReLU activations
- Dropout (p = 0.3)

#### Dual Output Heads
- **Classification Head:** Seizure vs Non-seizure
- **Regression Head:** Seizure onset & offset prediction

This method provides a strong interpretable baseline but struggles with complex temporal dependencies.

---

## 🤖 Method 2: CNN + BiLSTM + Attention (Deep Learning)

This method automatically learns spatial and temporal EEG representations.

### Model Components

#### 1. Instance Normalization
- Stabilizes training across patients and recording conditions

#### 2. Residual 1D CNN Layers
- Capture local temporal EEG patterns
- Residual connections prevent vanishing gradients

#### 3. BiLSTM (3 Layers)
- Models long-range temporal dependencies
- Processes EEG signals forward and backward in time

#### 4. Attention Mechanism
- Assigns importance weights to time steps
- Highlights seizure-relevant EEG regions

#### 5. Dual Output Heads
- **Classification:** Seizure probability
- **Regression:** Seizure onset & offset times

---

### Training Configuration

- Optimizer: Adam  
- Learning rate: 0.001  
- Dropout: 0.3  
- Epochs: 30  
- Stable convergence with minimal overfitting

---

## 🧠 Explainable AI (XAI) Techniques

Deep learning models are often criticized as “black boxes.”  
This project integrates **attention-based explainability** to address this issue.

### How XAI Works Here

- Attention scores are extracted during inference
- Scores are upsampled to match original EEG length
- Heatmaps are overlaid on EEG waveforms

### Interpretation

- **Bright regions:** High importance (model focus)
- **Dark regions:** Low contribution

These regions frequently align with clinically meaningful seizure activity.

---

### Benefits of XAI Integration

✔ Improves clinical trust  
✔ Validates model reasoning  
✔ Enhances transparency  
✔ Supports real-world medical adoption  

---

## 📈 Results Summary

| Method | Accuracy | F1-Score | Onset MAE | Offset MAE |
|------|--------|--------|----------|-----------|
| Feature-Based | 56.86% | 0.53 | 75.31 s | 124.89 s |
| CNN + BiLSTM + Attention | ~83% | +24% ↑ | Significantly lower | Significantly lower |

Method 2 outperforms Method 1 in **accuracy, robustness, and interpretability**.

---

## 🚀 Future Improvements

- Larger and more diverse EEG datasets
- Real-time seizure detection systems
- Patient-specific adaptive models
- Advanced XAI techniques (SHAP, saliency maps)
- Deployment-ready clinical pipelines

---

## 📚 Citation

If you use this work, please cite the associated paper.

---

## 🤝 Acknowledgments

This project was developed as part of an academic research initiative focused on applying AI to biomedical signal processing and clinical decision support.
---

