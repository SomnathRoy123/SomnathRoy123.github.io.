---
layout: page
title: Bio-Acoustic Event Detection via Spectral Contrast Enhancement
description: Detecting transient signals in high-noise environments using Background Subtraction and Convolutional Neural Networks.
img: assets/img/spectrogram_thumb.jpg
importance: 1
category: Machine Learning & Signal Processing
related_publications: false
repository: https://github.com/atharv-naik/whale-call-classification
date: 2023-04-20
---

**Role:** Algorithm Design & Optimization  
**Key Techniques:** `Spectral Subtraction` `Grid Search Optimization` `Ensemble Learning` `CNN`

## Project Abstract
In experimental physics and bio-acoustics, the primary challenge is often distinguishing a weak transient signal from a stochastic background. This project developed a computational pipeline to identify **Blue Whale A-Calls** by coupling classical signal processing (background subtraction) with deep learning (CNNs). The approach focuses on maximizing the Signal-to-Noise Ratio (SNR) *before* the data touches the neural network.

## 1. Mathematical Preprocessing: Spectral Contrast Enhancement
Standard spectrograms were insufficient due to ambient ocean noise. I implemented a **Dual-Domain Contrast Enhancement** algorithm to isolate the signal.

We treated the spectrogram $S(t, f)$ as a 2D scalar field and applied a moving average filter to subtract the background noise. We defined two distinct filters:

1.  **Temporal Filter (Horizontal):** Highlights short-duration events (transients) by removing steady-state noise over time $t$.
2.  **Frequency Filter (Vertical):** Highlights specific pitch anomalies by removing broadband noise across frequencies $f$.

The normalized signal $S'_{norm}$ was calculated by subtracting the local neighborhood mean ($\mu_{local}$) from the global neighborhood mean ($\mu_{global}$):

$$S'_{norm} = S_{raw} - \frac{\mu_{global} - \mu_{local}}{\sigma_{noise}}$$

This resulted in two distinct datasets (Time-Enhanced and Frequency-Enhanced), effectively doubling the training data and forcing the model to learn features that are invariant to background shifts.

## 2. Model Architecture & Optimization
We utilized a **Convolutional Neural Network (CNN)** to perform binary classification on the enhanced 64x64 spectral images. 

### Network Topology
* **Input:** 64x64 Single-Channel Spectrogram
* **Feature Extraction:** Two blocks of `Conv2D` (7x7 kernels) $\to$ `BatchNormalization` $\to$ `ReLU` $\to$ `MaxPooling`. Large kernels (7x7) were chosen specifically to capture the "chirp" structure of the whale calls.
* **Classifier:** Dense layers (200 units) with aggressive **Dropout (0.5)** to prevent overfitting on the small dataset.

### Hyperparameter Search (GridSearch)
Instead of manual tuning, I implemented a rigorous **GridSearchCV** to explore the hyperparameter phase space. We optimized for the **F1-Score** (harmonic mean of precision and recall) to handle class imbalance.

* **Optimizers Tested:** SGD, Adam, Adagrad, RMSprop
* **Learning Rates:** $10^{-1}, 10^{-2}$
* **Batch Sizes:** 128, 256, 384

**Optimal Configuration Found:**
* **Optimizer:** SGD (Stochastic Gradient Descent)
* **Activation:** ReLU
* **Batch Size:** 128

## 3. Inference Strategy: Ensemble Voting
To maximize robustness, the final classification was not based on a single pass. We employed an additive voting mechanism:

```python
# Inference Logic
Probability_Total = Model(Input_TimeEnhanced) + Model(Input_FreqEnhanced)
Prediction = 1 if Probability_Total > Threshold else 0