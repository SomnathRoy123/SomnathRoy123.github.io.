---
layout: page
title: Bio-Acoustic Event Detection in Stochastic Noise Fields
description: A study on identifying transient Blue Whale A-Calls using Dual-Domain Spectral Subtraction and Convolutional Neural Networks.
img: assets/img/spectrogram_thumb.jpg
importance: 1
category: Machine Learning
related_publications: false
repository: https://github.com/atharv-naik/whale-call-classification
date: 2023-04-20
---

**Role:** Computational Physics & Algorithm Design  
**Stack:** `Python` `TensorFlow/Keras` `Scikit-Learn` `Signal Processing`

## 1. Introduction: The Signal-to-Noise Challenge
In experimental bio-acoustics, the detection of specific animal vocalizations is often analogous to identifying a weak transient signal within a high-entropy, stochastic background. The **Blue Whale A-Call**—a low-frequency, pulsed vocalization—is frequently obscured by the ambient noise of the ocean, which follows a $1/f$ (pink noise) power spectral density, compounded by anthropogenic noise (shipping traffic) and other biological events.

This project implements a robust computational pipeline to solve this **binary classification problem**. By coupling classical signal processing (to improve the local Signal-to-Noise Ratio) with deep learning (for non-linear feature extraction), we achieve high-fidelity detection rates even in low-SNR environments.

## 2. Methodology: Dual-Domain Spectral Topology
Raw spectrograms are often insufficient for direct training due to the non-stationary nature of ocean noise. To address this, we treated the spectrogram $S(t, f)$ not merely as an image, but as a scalar field representing energy density. We applied a **Dual-Domain Contrast Enhancement** algorithm to isolate the signal from the background.

The background noise $\eta(t, f)$ is often correlated in one dimension but uncorrelated in the other:
* **Shipping Noise:** Continuous in time, localized in frequency (horizontal bands).
* **Impulsive Noise:** Localized in time, broadband in frequency (vertical spikes).

To filter this, we calculated the normalized signal intensity $S^\prime$ by subtracting the local neighborhood mean ($\mu_{\text{local}}$) from the global background mean ($\mu_{\text{global}}$), effectively performing a background subtraction in two orthogonal basis sets:

$$
S^\prime_{\text{norm}} = S_{\text{raw}} - \frac{\mu_{\text{global}} - \mu_{\text{local}}}{\sigma_{\text{noise}}}
$$

This resulted in two distinct datasets—**Time-Enhanced** and **Frequency-Enhanced**—forcing the neural network to learn features that are invariant to these specific noise topologies.



## 3. Neural Network Architecture
We constructed a **Convolutional Neural Network (CNN)** tailored specifically for the 64x64 spectral inputs. Unlike standard computer vision tasks that favor small (3x3) kernels, we opted for larger **7x7 convolutional kernels**.

### Physical Justification for 7x7 Kernels
The Blue Whale A-Call is not a point source; it is a "chirp" that evolves over time and frequency. A larger receptive field (7x7) allows the first layer of the network to capture the **long-range temporal and spectral correlations** of the call structure immediately, rather than relying on deeper layers to aggregate this information.

### Network Topology
The architecture was implemented in `Keras` with a custom `Scikit-Learn` wrapper for optimization:

1.  **Input Robustness:** A `Dropout(0.2)` layer is applied directly to the input. This introduces artificial noise during training, forcing the model to learn robust features that are not dependent on specific pixel artifacts.
2.  **Feature Extraction:**
    * **Layer 1:** 15 Filters ($7 \times 7$), Stride 1, `BatchNormalization`, `ReLU`, `MaxPooling` ($2 \times 2$).
    * **Layer 2:** 30 Filters ($7 \times 7$), Stride 1, `BatchNormalization`, `ReLU`, `MaxPooling` ($2 \times 2$).
3.  **Classification Head:** A fully connected `Dense` layer (200 units) with aggressive `Dropout(0.5)` to prevent overfitting, feeding into a final Sigmoid activation unit.

## 4. Hyperparameter Phase Space Search
To ensure the model was not falling into a local minimum, we avoided manual tuning. Instead, I implemented a rigorous **Grid Search (GridSearchCV)** to explore the hyperparameter phase space.

We defined a search grid over the following dimensions:
* **Optimization Algorithms:** `SGD`, `Adam`, `Adagrad`, `RMSprop`.
* **Learning Rates:** Logarithmic scale [$10^{-1}, 10^{-2}$].
* **Batch Dynamics:** Sizes of [128, 256, 384].

**Evaluation Metric:**
Given the sparsity of whale calls (class imbalance), accuracy is a poor metric. We optimized for the **F1-Score** (harmonic mean of precision and recall) and validated using the **ROC-AUC** (Area Under the Receiver Operating Characteristic Curve).

### Optimization Results
The search revealed that **Stochastic Gradient Descent (SGD)** with a high learning rate ($0.1$) and Nesterov momentum provided the most stable convergence, outperforming adaptive optimizers like Adam for this specific smooth-landscape problem.

## 5. Inference: The Logical 'OR' Gate
A key insight of this project was the use of **Ensemble Logic** during inference. The model makes predictions on both the *Time-Enhanced* and *Frequency-Enhanced* versions of the spectrogram.

We employed a logical disjunction (OR gate) for the final classification:
$$
\hat{y}_{\text{final}} = \hat{y}_{\text{time}} \lor \hat{y}_{\text{freq}}
$$

This means if the neural network detects a call in *either* the time-cleaned or frequency-cleaned domain, the event is flagged. This approach prioritizes **Recall (Sensitivity)**, which is critical in bio-acoustics where missing a rare biological event is often worse than a false positive.

<div class="mt-4">
    <a href="https://github.com/atharv-naik/whale-call-classification" class="btn btn-outline-dark btn-sm" role="button">
        <i class="fab fa-github"></i> View Full Repository
    </a>
</div>