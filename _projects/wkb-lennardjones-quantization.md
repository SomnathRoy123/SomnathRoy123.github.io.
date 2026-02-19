---
layout: page
title: WKB Quantization of the Lennard-Jones Potential
description: Semi-classical computation of bound-state spectra in the Lennard-Jones potential using WKB methods, turning molecular interaction physics into a reproducible numerical workflow.
importance: 2
category: Computational Data Science
related_publications: false
repository: https://github.com/SomnathRoy123/WKB-LennardJones-Quantization
date: 2024-09-10
---

**Role:** Theoretical Modeling & Numerical Implementation  
**Stack:** `Python` `NumPy` `SciPy` `Matplotlib` `WKB Approximation`

## 1. Introduction: Why Semi-Classical Quantization Matters

The Lennard-Jones potential is a foundational model in atomic and molecular physics, capturing the competition between short-range repulsion and long-range attraction. This project studies how far one can push a **semi-classical (WKB)** treatment to recover the structure of bound states for such a nontrivial potential landscape.

Instead of treating quantization as a symbolic-only exercise, the repository frames it as a computational pipeline: define turning points, evaluate the action integral, impose quantization, and compute the energy spectrum with controlled numerical precision.

## 2. Methodology: From Potential Landscape to Energy Levels

For a trial energy $E$, the classical turning points $r_1, r_2$ are obtained from $V(r)=E$. The WKB quantization condition is then enforced:

$$
\int_{r_1}^{r_2} \sqrt{2\mu\,(E - V(r))}\,dr = \left(n+\frac{1}{2}\right)\pi\hbar
$$

The code numerically solves this condition across quantum numbers to estimate the bound-state ladder and inspect spacing trends.

### Key computational components

- Robust turning-point detection for each admissible $E$.
- Stable quadrature of the action integral near endpoint singular behavior.
- Root-finding loop that maps each quantum index to a unique energy level.

## 3. Outcomes and Scientific Value

- Constructed a reproducible framework to estimate bound-state energies in a physically relevant interaction potential.
- Demonstrated how semi-classical methods can bridge analytical physics intuition with practical numerical computation.
- Produced publication-ready diagnostics showing quantization consistency and spectral structure.

## 4. Why this strengthens a PhD profile

This project highlights the ability to combine **advanced analytical physics concepts** with **careful numerical implementation**, which is essential in graduate research spanning quantum systems, statistical mechanics, and computational modeling.

<div class="mt-4">
    <a href="https://github.com/SomnathRoy123/WKB-LennardJones-Quantization" class="btn btn-outline-dark btn-sm" role="button">
        <i class="fab fa-github"></i> View Full Repository
    </a>
</div>
