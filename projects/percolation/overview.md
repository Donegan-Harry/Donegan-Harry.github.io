---
layout: percolation
title: Overview
---

Percolation is conceptually easy (relative to most physics and maths concepts) yet its simplcity does not extend to solving it. For this reason, we are giving an overview at first which will detail all the quantities of interest and their general behaviour. The technical details of how we actually go about solving them will be the vast bulk of the work which will follow in the subsequent pages.


A lattice is said to be percolating if an infinite cluster spans the system, it thus has two  distinct phases: non-percolating and percolating. The **percolation threshold** (critical point) $p_{c}$ of the transition is the probability at which the system is first percolating and sets the transition point between the two phases. 

The **order parameter** (percolation strength) measures how much of the system belongs to the percolating phase. We define it as the number of sites belonging to the infinite cluster $n_{\infty}$ to the total number of sites $N$ in the limit of an infinite system

$$ P_{\infty} = \lim_{N\rightarrow\infty} \frac{n_{\infty}}{N}. $$

This quantity is zero in the non-percolating phase ($p < p_{c}$) and positive in the percolating phase ($p > p_{c}$). 

As the occupation probability increases from zero, clusters consisting of nearest-neighbor connections begin to form. These clusters have varying sizes $s$ and can be characterised by their number densities $n_{s}$, the number of clusters of size $s$ per lattice site. A fundamental quantity associated with the transition is the **susceptibility** (mean cluster size)

$$ S = \frac{\sum_{s\neq\infty}s^2n_{s}}{\sum_{s\neq\infty}sn_{s}}. $$

Approaching the critical point, this quantity will diverge as the clusters begin to conglomerate into the infitnite cluster. Away from the critical point, the mean cluster size is finite and the quantity always appears as a large spike when traversing $p$. Note that this quantity is not directly measuring the spatial extent of the clusters but more how many sites belong to a cluster.

To measure the spatial extent of the clusters we use the **correlation length** which is a measure of the connectedness of the system. This is calculated via the correlation function $g(r)$ which is the probability that two sites seperated by a distance $r$ belong to the same cluster

$$ g(r) = \frac{1}{p} \langle n(0) \cdot n(\mathbf{r}) \cdot \mathbb{1}_{\text{same cluster}} \rangle, $$

where n(x) = 1 if site x is occupied and 0 otherwise, and the indicator function ensures both sites belong to the same cluster. The correlation length sets the fundamental length scale for the percolation transition, away from the critical point we expect the correlation length to be small and the correlation length to decay exponentially

$$g(r)\propto\exp\left(-\frac{r}{\xi}\right)$$ 

as the clusters appear isolated from eachother and the connectedness is low. Of course at the transition point, the entire system is connected and we expect that $\xi\rightarrow\infty$ as the cluster spans everywhere.

Near the percolation threshold, the system exhibits a continuous phase transition which is characterised by scale invariance. The system looks the same on all length scales. A most remarkable feature of this transition is that the observables that we have mentioned all exhibit power-law behaviour governed by **critical exponents**. We find that in the vicnity of $p_{c}$ the order paramter scales as $P_{\infty}\sim(p-p_{c})^{\beta}$, and the susceptibility and correlation lengths diverge as $S\sim\vert p-p_{c}\vert^{-\gamma}$ and $\eta\sim\vert p-p_{c}\vert^{\eta}.$ The regime where this occurs is known as criticality and other quantities exhbit power-law behaviour with the correlation length decaying in power law fashion as 

$$g(r)\sim r^{-(d-2+\eta)}$$

where $d$ is the dimensionality of the system. Perhaps most telling of all of these quantities is the number density $n_{s}$ which scales as $s^{-\tau}$ which indicates that clusters of all sizes form.



