---
layout: percolation
title: Bethe Lattice
---

Despite the simplicity of the percolation model, it is notoriously difficult to solve exactly on even the simplest lattices (with the trivial exception of one dimension, which we will discuss later). The difficulty is that on a general lattice the presence of loops introduces correlations between sites, destroying statistical independence and placing an exact solution beyond our current means. It should therefore come as no surprise that the lattice on which an exact solution can be derived precludes any loops in its geometry. The Bethe lattice is an infinite connected cycle-free lattice where each vertx has $z$ neighbours ($z$ is known as the coordination number). It can be constructed by starting from a central vertex with $z$ bonds; at the end of each bond, an additional $z-1$ bonds emerge, with the remaining bond connecting back toward the origin. This branching process is continued onwards.
