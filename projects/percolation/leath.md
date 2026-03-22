---
layout: percolation
title: Leath Algorithm
---

An alternative numerical implementation for percolation is the Leath algorithm. Unlike the Hoshen–Kopelman method, which identifies all clusters in a lattice, the Leath algorithm generates a single cluster grown from a seed site. The procedure is analogous to epidemic spreading: starting from an initially occupied site (usually at the centre), its nearest neighbours are tested and each is occupied with probability $p$, or left unoccupied with probability $1-p$. This process is then applied recursively: for each newly occupied site, its neighbours are tested in the same way. The cluster continues to grow outward until no new occupied sites are added (the cluster dies out) or a system boundary is reached.

An implementation for a square lattice reads 
```julia
function Leath(L, p)
    Lattice = zeros(L, L)
    
    # Initiate the lattice with an occupied site in the centre
    seed_idx = div(L, 2) + 1
    Lattice[seed_idx, seed_idx] = 1

    function Grow(idx, idy, L)
        neighbours = []
        # Potential neighbors
        potential_neighbours = [
        (idx-1, idy), # Left
        (idx+1, idy), # Right
        (idx, idy-1), # Down
        (idx, idy+1)  # Up
        ]

        for (nx, ny) in potential_neighbours
        # Check if the neighbor is within the grid boundaries
            if 1 <= nx <= L && 1 <= ny <= L
                push!(neighbours, (nx, ny))
            end
        end
    
        return neighbours
    end

    boundary = Grow(seed_idx, seed_idx, L)

    while !isempty(boundary) 
        new_boundary = []
        for site in boundary
            idx, idy =  site

            # Check if site has already been visited
            if Lattice[idx, idy] !=0 
                continue 
            end

            p_site = rand()
            if p_site < p 
                Lattice[idx, idy] = 1
                neighbours = Grow(idx, idy, L)
                
                for neighbour_site in neighbours
                    n_idx, n_idy = neighbour_site
                    # Only add unvisted sites to the boundary
                    if Lattice[n_idx, n_idy] == 0 
                        push!(new_boundary, neighbour_site)
                    end
                end
            else 
                Lattice[idx, idy] = -1
            end
        end
        # Update new boundary and remove duplicates
        boundary = unique(new_boundary)
    end
    
    # Remove the labelling of -1 
    replace!(Lattice, -1 => 0)
    return Lattice
end
```
