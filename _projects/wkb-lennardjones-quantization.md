---
layout: page
title: Numerical WKB Quantization of Lennard-Jones Systems
description: A computational framework for solving the Bohr-Sommerfeld quantization condition to predict the energy spectra of molecular van der Waals interactions.
importance: 1
category: Computational Data Science
related_publications: false
repository: https://github.com/SomnathRoy123/WKB-LennardJones-Quantization
date: 2024-09-10
---

**Role:** Theoretical Modeling & Lead Developer  
**Stack:** `Python` `NumPy` `SciPy (Optimize & Integrate)` `Matplotlib`

## 1. Project Objective: Bridging Analytical Theory & Simulation
The primary goal was to develop an automated pipeline to calculate the **discrete energy levels ($E_n$)** of a particle trapped in a Lennard-Jones (12-6) potential. This problem lacks a closed-form analytical solution, making it a perfect candidate for demonstrating how **semi-classical (WKB) physics** can be turned into a reproducible numerical workflow.

## 2. Coding Logic & Numerical Architecture
The code is structured into a functional pipeline designed for numerical stability and precision:

* **The Potential Engine:** Implemented the Lennard-Jones potential $V(r)$ using vectorized `NumPy` operations to allow for efficient energy-surface mapping.
* **Turning-Point Algorithm:** Used `scipy.optimize.brentq` to solve for $r_1$ and $r_2$. I handled the **steep repulsive wall** at small $r$ by constraining the search interval, preventing the root-finder from diverging into the $r \to 0$ singularity.
* **The Action Integral:** Built a robust integration loop to evaluate:
    $$\int_{r_1}^{r_2} \sqrt{2\mu(E - V(r))}\,dr = (n + \frac{1}{2})\pi\hbar$$
    I utilized `scipy.integrate.quad` with an increased number of sub-intervals (`limit=100`) to manage the **inverse-square root singularity** that occurs at the turning points.
* **Energy Level Iteration:** Developed a "Spectral Search" loop that iterates through quantum numbers $n$, finding the specific energy $E$ for each $n$ that satisfies the quantization condition.

## 3. Results & Scientific Value
* **Anharmonic Spectrum:** Successfully mapped the energy levels, showing how the "ladder" gets closer together as the energy approaches the dissociation limit—a hallmark of real molecular bonds.
* **Validation:** Generated publication-ready plots using `Matplotlib` that overlay the energy levels on the potential well, confirming the physical consistency of the results.

## 4. Conclusion: Research Impact
This project demonstrates my ability to take a high-level physics theory and implement a **production-ready numerical solution**. By solving the challenges of singularity-handling and non-linear root finding, I have built a toolkit directly applicable to my PhD goals in **Biophysics**, specifically for modeling **nuclear dynamics** and **protein-ligand interaction potentials** under mechanical stress.

<div class="mt-4">
    <a href="https://github.com/SomnathRoy123/WKB-LennardJones-Quantization" class="btn btn-outline-dark btn-sm" role="button">
        <i class="fab fa-github"></i> Explore the Code
    </a>
</div>