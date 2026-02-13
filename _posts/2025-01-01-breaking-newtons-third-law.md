---
layout: post
title: "Breaking Newton's Third Law: The Physics of Non-Reciprocal Interactions"
date: 2025-01-01 09:00:00
description: When Action ≠ Reaction. Exploring how non-reciprocity drives emergent behavior in active matter, from bacterial swarms to neural networks.
tags: active-matter non-equilibrium-physics theory research
categories: research
featured: true
thumbnail: assets/img/active_matter_thumb.jpg  # Replace with a snapshot of your simulation!
---

In standard equilibrium physics, interactions are almost always reciprocal. If Particle A pushes Particle B, Particle B pushes back with equal force. This is Newton’s Third Law, and it allows us to define conserved quantities like momentum and energy.

But biology does not care about Newton's Third Law.

In my current research on **Active Matter**, I am investigating systems where $F_{AB} \neq -F_{BA}$. These are **non-reciprocal interactions**, and they are the secret engine behind some of nature's most complex self-organizing systems.

### The Predator-Prey Archetype

 The simplest way to understand non-reciprocity is the relationship between a predator and its prey.
* **The Predator ($P$)** is attracted to the Prey ($p$).
* **The Prey ($p$)** is repelled by the Predator ($P$).



In a conservative physical system, this would be impossible; forces are gradients of a shared potential energy. But in active matter, each agent consumes energy individually. This breaks the symmetry. The result is a **constant pursuit**, a non-equilibrium steady state where the system never "settles down" into a static configuration.

### From Chasing to Time-Crystals

When we scale this up from two particles to thousands, the behavior becomes fascinatingly complex. In my Master's thesis work, we model these interactions using **Overdamped Langevin Dynamics** with generalized interaction matrices.

We observe that as the degree of non-reciprocity increases (i.e., as the system becomes more asymmetric), the system undergoes phase transitions that don't exist in passive matter:

1.  **Traveling Waves:** Density fluctuations that propagate through the crowd like sound waves, but driven entirely by the internal asymmetry of the agents.
2.  **Chiral Phases:** Spontaneous rotation of clusters. Even if the individual particles have no "spin," the group angular momentum becomes non-zero purely due to the non-reciprocal forces.
3.  **Time-Crystalline Order:** Patterns that repeat in time, not just in space. The system cycles through states without ever reaching a halt.

### Biological Relevance: Why Study This?

This isn't just a mathematical curiosity. Non-reciprocity is fundamental to living tissue.

* **Neural Networks:** A neuron $A$ excites neuron $B$, but neuron $B$ inhibits neuron $A$. This asymmetry is crucial for generating brain waves and processing information.
* **Chemotaxis:** Bacteria release chemical trails that attract others, but they might consume the attractant, creating a complex, non-symmetric interaction landscape.
* **Immune Response:** Immune cells chase pathogens (attraction), while pathogens evolve mechanisms to evade detection (repulsion).



[Image of neural network synapse diagram]


### The Theoretical Challenge

The breakdown of reciprocity means we lose the ability to use standard Boltzmann statistics. There is no "Free Energy" to minimize.

Instead, we have to rely on tools from **Non-Linear Dynamics** and **Stochastic Thermodynamics**. We look for "exceptional points" in the dynamical spectrum where eigenvalues coalesce, signaling a transition from static behavior to oscillatory or chaotic motion.

### Conclusion

My research aims to quantify these transitions. By mapping the phase diagram of non-reciprocal active matter, we hope to understand the generic rules that allow "dumb" biological agents to form "smart," resilient structures.

It turns out that breaking Newton's Third Law isn't just allowed in biology—it's necessary.