---
layout: percolation
title: Leath Algorithm
---

Getting percolation to work on a computer is actually rather simple. We need only initialise a zero array (in fact we only need a bit matrix) whose elements correspond to sites on the lattice and then use a random number generator to flip some of these elements to one. And just like that, we have a digital implementation of percolation. A percolation problem on a square lattice can easily be generated via
