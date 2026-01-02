---
layout: percolation
title: Monte-Carlo Simulation
---

Now we have a computer simulation of percolation with a cluster-identifying sub-routine we are free to investigate quantities of interest to our hearts desire. In general we will be interested in the the $p$-dependence of expectation values $\langle X \rangle$. The expectation value of a quantity $X$ at $p$ can be calculated using the sample mean of a lot of repeated numerical 'experiments'. Thus conducting the percolation multiple times we have

$$\langle X \rangle \approx \overline{X} = \frac{1}{M}\sum_{i} X_{i}, $$

where the result can only be trusted within any statistical errors given by the standard error in the mean

$$ \Delta X = \frac{1}{M} \sqrt{\overline{X^2}-\overline{X}^2}.$$

For example, we can look at the first percolation quantity introduced: the infinite cluster strength $P_{\infty}$. We define $P_{\infty}$ in this instance as the expectation value of $n_{\infty}/N$ where $n_{\infty}$ is the number of sites belonging to the 'infinite' cluster and $N$ is the total number of sites ($L^2$ for the square lattice). Such a quantity requires us to find the 'infinite' cluster which is actually quite simple. We need only find if the opposite edge rows or columns share any common labels and if they do we have found our infinite cluster, the label and the corresponding size. The following functions implement the necessary calculations:

```julia
function isPercolating(M)
    # Retrieve edges of system
    top_edge = M[1, :]
    bottom_edge = Set(M[end, :])
    left_edge = Set(M[:, 1])
    right_edge = M[:, end]

    # Check if cluster spans system top to bottom (exclude zeros)
    vertical = findfirst(k -> k != 0 && k in bottom_edge, top_edge)
    if vertical !== nothing 
        return true, top_edge[vertical] 
    end 

    # Check if cluster spans system left to right (exclude zeros)
    horizontal = findfirst(k -> k != 0 && k in left_edge, right_edge)
    if horizontal !== nothing 
        return true, right_edge[horizontal] 
    else 
        return false, nothing
    end
end


function PercolationStrength(L, mc_num)
    p = range(0, 1, 100)
    order = zeros(length(p))
    order_uncertainity = zeros(length(p))
    for i in 1:length(p)
        mc_values = zeros(mc_num)
        for j in 1:mc_num
            M = SquareLattice(L, p[i])
            HK_M = HK(M)
            phase, cluster_id = isPercolating(HK_M)
            mc_values[j] = (cluster_id === nothing) ? 0 : count(==(cluster_id), HK_M) / L^2
        end
        order[i] = mean(mc_values)
        order_uncertainity[i] = std(mc_values)
    end
    return order, order_uncertainity
end
```

Running the above code for a square lattice, we compute a representative example (Figure 3) of the percolation order parameter. At current sizes, we find that the threshold for site percolation on a square lattice is $p_{c}\approx 0.58$. The most accurate determination on this threshold is currently $p_{c} = 0.592 746 050 792 10(2)$ so our simulation is clearly in the right ball park. We of course do not have a very large system $L=250$ is very far from inifinite but we will later discuss some other methods to calculate this threshold.

<p style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/images/percolation/PercolationOrderParameter_Square.svg" alt="PercolationOrderParameter_Square" style="max-width: 600px;">
</p>

<p style="text-align: center; color: #666; font-size: 0.95em; font-style: italic; margin-top: 0.5rem;">
  Figure 3: Percolation strength on a square lattice of length $L=250$ calculated using Monte-Carlo methods with $M=1000$ samples taken for each $p$ value.
</p>

Another basic property we can calculate is the mean cluster size $S$. This quantity is defined by

$$
S = \frac{\sum_{s\neq\infty}s^2n_{s}}{\sum_{s\neq\infty}sn_{s}},
$$

where $n_{s}$ is the number of finite clusters of size $s$, note that we exclude the presence of any system-spanning (infinite) clusters. We can implement the mean cluster size with the following function 

```julia
function MeanClusterSize(L, mc_num)
    p = range(0, 1, 100)
    Size = zeros(length(p))
    Size_uncertainity = zeros(length(p))
    for i in 1:length(p)
        mc_values = zeros(mc_num)
        for j in 1:mc_num
            M = SquareLattice(L, p[i])
            HK_M = HK(M)
            phase, cluster_id = isPercolating(HK_M)
            # Find the multiplicity of clusters (exclude non-occupied sites and infinite cluster)
            clusters = filter(x -> x != 0 && x != cluster_id, unique(HK_M))
            cluster_num = [count(==(x), HK_M) for x in clusters]
            # Calculate the mean cluster size
            mc_values[j] = isempty(cluster_num) ? 0 : sum(cluster_num.^2)/sum(cluster_num)
        end
        Size[i] = mean(mc_values)
        Size_uncertainity[i] = std(mc_values)/sqrt(mc_num)
    end
    return Size, Size_uncertainity
end
```

As we run this code on the square lattice (Figure 4), we see the appearance of a large spike in the mean cluster size as the system approaches the percolation threshold. 

<p style="text-align: center; margin: 1.5rem 0;">
  <img src="/assets/images/percolation/MeanClusterSize_Square.svg" alt="MeanClusterSize_Square" style="max-width: 600px;">
</p>

<p style="text-align: center; color: #666; font-size: 0.95em; font-style: italic; margin-top: 0.5rem;">
  Figure 4: Mean (finite) cluster size on a square lattice of length $L=250$ calculated using Monte-Carlo methods with $M=1000$ samples taken for each $p$ value.
</p>
