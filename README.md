# 🧠 Data-Driven Epileptic Seizure Detection from EEG  
### With Complementary Explainable AI (XAI) Analysis

---

## 📌 Overview

Epileptic seizure detection from Electroencephalography (EEG) signals is a critical task in clinical neuroscience. Manual EEG interpretation is time-consuming, subjective, and prone to error due to the complex temporal dynamics of brain activity.

This project presents a **comparative, data-driven framework** for automated seizure detection and seizure onset–offset localization using EEG signals. Two complementary approaches are explored:

1. **Classical signal processing with handcrafted features**
2. **A deep learning architecture combining CNN, BiLSTM, and Attention**

To ensure **clinical transparency and trust**, we integrate **Explainable Artificial Intelligence (XAI)** techniques that visually highlight which EEG regions influence the model’s decisions.

---

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

- 50 Hz IIR notch filter  
- FIR bandpass filter (0.5–70 Hz)  
- Resampling to 250 Hz  
- Channel selection (6 channels)  
- Sliding window segmentation  

---

## 🔄 Data Pipeline

Raw EEG → Filtering → Resampling → Segmentation → Model Input

---

## 🧪 Method 1: Feature-Based Model

- Frequency-domain features: Delta, Theta, Alpha, Beta, Gamma  
- Time-domain features: Mean, Std, RMS, Skewness, Kurtosis  
- Total features: 60  

Fully connected network with classification and regression heads.

---

## 🤖 Method 2: CNN + BiLSTM + Attention

- Residual 1D CNN layers  
- 3-layer BiLSTM  
- Attention mechanism for interpretability  
- Dual output heads (classification + regression)

---

## 🧠 Explainable AI (XAI)

Attention weights are visualized as heatmaps over EEG signals, highlighting seizure-relevant regions and improving clinical trust.

---

## 📈 Results Summary

Feature-based model provides a baseline, while the CNN–BiLSTM–Attention model achieves significantly higher accuracy and better onset–offset localization.

---

## 🚀 Future Work

- Larger datasets  
- Real-time detection  
- Patient-specific models  
- Advanced XAI methods

