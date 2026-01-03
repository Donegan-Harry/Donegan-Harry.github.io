---
layout: percolation
title: Overview
---

Percolation is conceptually easy (relative to most physics and maths concepts) yet its simplcity does not extend to solving it. For this reason, we are giving an overview at first which will detail all the quantities of interest and their general behaviour. The technical details of how we actually go about solving them will be the vast bulk of the work which will follow in the subsequent pages.

A lattice is said to be percolating if an infinite cluster spans the system, it thus has two phases: non-percolating and percolating. The **percolation threshold** (critical point) $p_{c}$ of the transition is the probability at which the system is first percolating and sets the transition point between the two phases. This also lets us introduce the notion of an **order parameter** (percolation strength) which measures how much of the system belongs to this phase, we may define it as the number of sites belonging to the infinite cluster $n_{\infty}$ to the total number of sites $N$ in the limit of an infinite system

$$ P_{\infty} = \lim_{N\rightarrow\infty} \frac{n_{\infty}}{N}. $$

As the probability is increased from $0$, clusters consiting of nearest-neighbour connections begin to form. These clusters will have a size $s$ and can be grouped into number densities $n_{s}$, that is the number of clusters of size $s$ in the lattice. A natural quantity to study in the transition is the mean cluster size $S$, also known as the **susceptability** 

$$ S = \frac{\sum_{s\neq\infty}s^2n_{s}}{\sum_{s\neq\infty}s^2n_{s}}. $$

