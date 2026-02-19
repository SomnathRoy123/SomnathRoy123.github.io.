---
layout: page
title: Unsupervised Spatial Clustering of Orion YSOs
description: A machine-learning pipeline for structural analysis of high-dimensional spatial data, utilizing Minimum Spanning Trees (MST) and DBSCAN clustering on Gaia DR3 astrometry.
importance: 3
category: Computational Data Science
related_publications: false
repository: https://github.com/SomnathRoy123/Orion-YSO-Structure
date: 2024-12-01
---

**Role:** Data Scientist & Statistical Modeler  
**Stack:** `Python` `Pandas` `SciKit-Learn (DBSCAN)` `NetworkX (MST)` `Matplotlib` `Jupyter`

## 1. Project Objective: Pattern Recognition in Noisy Environments
Identifying Young Stellar Objects (YSOs) in the Orion Complex requires extracting meaningful structural features from millions of background data points. The goal of this project was to build a reproducible, data-driven pipeline to quantify spatial clustering, moving beyond visual estimation to robust statistical validation. 



This challenge—identifying sub-structures within a noisy, heterogeneous environment—is mathematically identical to mapping protein aggregates in a cell or classifying cellular distributions in tissue samples.

## 2. Coding Logic & Algorithmic Approach
Instead of relying on basic distance thresholds, this repository implements advanced unsupervised machine learning techniques to characterize spatial morphology:

* **Big Data Ingestion:** Processed and cleaned high-dimensional astrometric data from the **Gaia DR3** catalog, handling missing values, coordinate transformations, and measurement uncertainties.
* **Density-Based Clustering (DBSCAN):** Deployed `scikit-learn`'s DBSCAN algorithm to identify core YSO clusters. This method was specifically chosen because it does not require a pre-defined number of clusters ($k$) and gracefully handles the heavy background "noise" of non-YSO stars.
* **Structural Graphing (MST):** Constructed a **Minimum Spanning Tree** over the spatial coordinates to compute the $Q$-parameter (the ratio of normalized mean edge length to correlation length). This allowed for the quantitative distinction between centrally condensed clusters and fractal-like, sub-clustered environments.

## 3. Results & Technical Outcomes
* **Automated Sub-structure Detection:** Successfully segregated the Orion complex into distinct morphological sub-regions, validating the pipeline's ability to detect varying density gradients.
* **Scalable Framework:** The analysis code is modularized so that updated catalog parameters or entirely new target fields can be processed through the same clustering logic with minimal manual intervention.

## 4. Conclusion: Value for Interdisciplinary Research
This project demonstrates my proficiency in **handling large, messy datasets** and extracting physical meaning using **modern machine learning tools**. The ability to construct graph-based models (MST) and density-based clusters (DBSCAN) is highly transferable. Whether the data points represent stars in a nebula or the spatial coordinates of **cell nuclei under mechanical stimuli**, the statistical principles of pattern recognition remain the same—making this toolkit directly applicable to my future PhD research in biophysics.

<div class="mt-4">
    <a href="https://github.com/SomnathRoy123/Orion-YSO-Structure" class="btn btn-outline-dark btn-sm" role="button">
        <i class="fab fa-github"></i> Explore the Jupyter Notebooks
    </a>
</div>