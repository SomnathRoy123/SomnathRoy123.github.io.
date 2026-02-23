---
layout: page
title: Emergent Behaviors in Active Systems Driven by Non-Reciprocal Torques
description: A theoretical and computational investigation into how breaking Newton's third law in active matter systems drives novel dynamical phase transitions.
importance: 1
category: Biophysics
related_publications: false
date: 2025-05-01
---

**Role:**Visiting student researcher 
**Institution:** Technische Universität Berlin (Group of Prof. Holger Stark) & IISER Kolkata  
**Stack:** `C/C++` `Python (Data Analysis)` `HPC/MPI`

## 1. Theoretical Background: Active Brownian Particles
The physical foundation of this project is based on **Active Brownian Particles (ABPs)**. Unlike classical passive particles driven purely by thermal fluctuations, ABPs are non-equilibrium agents that constantly convert energy into directed motion along an internal orientation axis. This continuous self-propulsion is subjected to rotational diffusion, resulting in persistent random walks. 



A hallmark of standard ABP systems is **Motility-Induced Phase Separation (MIPS)**. Even in the absence of attractive forces, purely repulsive steric interactions cause these self-propelled particles to spontaneously separate into dense solid-like clusters and dilute gas-like regions. This occurs because particles collide and temporarily block each other's paths faster than their orientation can diffuse away.

## 2. The Research Goal: Breaking Action-Reaction Symmetry
The primary objective of my thesis was to investigate what happens to this macroscopic collective behavior when we break Newton's third law at the microscopic interaction level. 

In biological systems, interactions are rarely reciprocal. For example, when two *Chlamydomonas* algae interact, their flagella sterically hit each other or nearby surfaces, exerting avoidant torques that depend heavily on their relative orientations. To model this, we introduced **non-reciprocal orientational interactions** into the standard ABP model. In our mathematical framework, the torque $\tau_{ij}$ exerted by particle $j$ on particle $i$ is not equal and opposite to $\tau_{ji}$ ($\tau_{ij} \neq -\tau_{ji}$). 



This fundamental breaking of action-reaction symmetry—and by extension, parity and time-reversal symmetries—provides a theoretical mechanism to circumvent traditional MIPS and engineer entirely new forms of collective self-organization.

## 3. Key Findings & Phase Transitions
Through extensive systematic mapping of the parameter space, we uncovered several distinct dynamical regimes:
* **Disruption of MIPS:** As expected, introducing strong avoidant non-reciprocal torques generally prevents particles from clustering, effectively melting the MIPS state into a disordered, homogeneous gas.
* **Emergent Flocking:** The most striking discovery occurred when the range of the non-reciprocal torques was tuned to closely match the steric exclusion range. Under these specific spatial conditions, the active particles spontaneously self-organized into highly coherent, collectively moving flocks.
* **Structural Polymorphism:** We characterized these flocking states quantitatively, demonstrating that the system exhibits a variety of structural forms—spanning from single, highly dense macroscopic bands to highly dynamic, moderately-dense porous stripes.

## 4. Computational Methodology
To capture these large-scale macroscopic behaviors and validate the theory, I developed an optimized numerical simulation engine:
* **Overdamped Langevin Dynamics:** The core physics engine solved coupled stochastic differential equations for the translational and orientational degrees of freedom, integrating thermal noise and active propulsion mechanics.
* **Algorithmic Optimization:** To simulate statistically significant ensemble sizes over long biological timescales, the force-calculation architecture was optimized using localized spatial binning and neighbor-list algorithms, significantly reducing computational overhead.
* **Distributed Computing:** The framework was deployed on High-Performance Computing (HPC) clusters to conduct massive parallel sweeps of the parameter space (torque amplitude vs. interaction range) to accurately plot the macroscopic phase boundaries.

---
layout: page
title: Emergent Behaviors in Active Systems Driven by Non-Reciprocal Torques
description: A theoretical and computational investigation into how breaking Newton's third law in active matter systems drives novel dynamical phase transitions.
importance: 1
category: Computational Physics & Biophysics
related_publications: true
repository: [Link to your GitHub - Optional]
date: 2024-05-01
---

**Role:** Theoretical Modeling & Computational Researcher  
**Institution:** Technische Universität Berlin (Group of Prof. Holger Stark) & IISER Kolkata  
**Stack:** `C/C++` `Python (Data Analysis)` `HPC/MPI`

## 1. Theoretical Background: Active Brownian Particles
The physical foundation of this project is based on **Active Brownian Particles (ABPs)**. Unlike classical passive particles driven purely by thermal fluctuations, ABPs are non-equilibrium agents that constantly convert energy into directed motion along an internal orientation axis. This continuous self-propulsion is subjected to rotational diffusion, resulting in persistent random walks. 



A hallmark of standard ABP systems is **Motility-Induced Phase Separation (MIPS)**. Even in the absence of attractive forces, purely repulsive steric interactions cause these self-propelled particles to spontaneously separate into dense solid-like clusters and dilute gas-like regions. This occurs because particles collide and temporarily block each other's paths faster than their orientation can diffuse away.

## 2. The Research Goal: Breaking Action-Reaction Symmetry
The primary objective of my thesis was to investigate what happens to this macroscopic collective behavior when we break Newton's third law at the microscopic interaction level. 

In biological systems, interactions are rarely reciprocal. For example, when two *Chlamydomonas* algae interact, their flagella sterically hit each other or nearby surfaces, exerting avoidant torques that depend heavily on their relative orientations. To model this, we introduced **non-reciprocal orientational interactions** into the standard ABP model. In our mathematical framework, the torque $\tau_{ij}$ exerted by particle $j$ on particle $i$ is not equal and opposite to $\tau_{ji}$ ($\tau_{ij} \neq -\tau_{ji}$). 



This fundamental breaking of action-reaction symmetry—and by extension, parity and time-reversal symmetries—provides a theoretical mechanism to circumvent traditional MIPS and engineer entirely new forms of collective self-organization.



## 4. Computational Methodology
To capture these large-scale macroscopic behaviors and validate the theory, I developed an optimized numerical simulation engine:
* **Overdamped Langevin Dynamics:** The core physics engine solved coupled stochastic differential equations for the translational and orientational degrees of freedom, integrating thermal noise and active propulsion mechanics.
* **Algorithmic Optimization:** To simulate statistically significant ensemble sizes over long biological timescales, the force-calculation architecture was optimized using localized spatial binning and neighbor-list algorithms, significantly reducing computational overhead.
* **Distributed Computing:** The framework was deployed on High-Performance Computing (HPC) clusters to conduct massive parallel sweeps of the parameter space (torque amplitude vs. interaction range) to accurately plot the macroscopic phase boundaries.


## 5. High-Performance Computing (HPC) Architecture
To simulate large systems of ABPs over extensive biological timescales, I developed a highly parallelized codebase from scratch in `C`, optimized for deployment on distributed-memory HPC clusters.

* **MPI Parallelization:** Designed a Master-Worker node architecture using the Message Passing Interface (`MPI_COMM_WORLD`, `MPI_Bcast`, `MPI_Send/Recv`). The simulation domain was spatially decomposed, dividing the scalar computational load ($N$ particles) across multiple processing cores to drastically reduce runtime for large $N$.
* **$\mathcal{O}(N)$ Force Computation:** Implemented a dual-layered optimization strategy utilizing **Cell-Linked Lists** and **Verlet Neighbor Lists**. By binning particles into a spatial grid and restricting pairwise distance calculations to adjacent bins, the computational time complexity of the force calculation was reduced from $\mathcal{O}(N^2)$ to $\mathcal{O}(N)$.
* **Memory & I/O Management:** Engineered dynamic memory allocation for particle coordinates, force arrays, and neighbor lists to ensure no memory leaks during long, multi-day cluster runs. I/O operations were optimized to periodically dump simulation state data for offline analysis.

