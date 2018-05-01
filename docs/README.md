# MonteIsing
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
## ToC
- [Overview](#overview)
- [Run](#run)
- [Lattice Class](#lattice-class)
- [DrawLattice Class](#drawlattice-class)
- [Structure of the Lattice](#structure-of-the-lattice)
- [Multidimensional Neighbours Interactions and Counting](#multidimensional-neighbour-interactions-and-counting)

## Overview

## Run

To run open `root` and run `.x compileMacro.C`. You can try
the axamples loading with `.L`.

## Lattice Class

The class can build a multi dimensional square lattice of spins.

$$ H = - \sum_{\langle i, j\rangle}^{}J_{ij} \sigma_i \sigma_j - \mu \sum_{i=1}^{N} \sigma_i $$

$$ J_{ij} = 1 \text{ and } \mu = 1 $$

## DrawLattice Class

The class can draw 2D or 3D lattice from the class Lattice.

![Cooling 2D 1][cooling2D-1] ![Cooling 2D 2][cooling2D-2]
![Cooling 2D 3][cooling2D-3] ![Cooling 2D 4][cooling2D-4]

1000000 spin 2D model at $$ T \approx 0.5 $$. Each frame is the flipping
of 1000 spins. First video goes from 0 to 20000th iterations, then
each gif continues with the next 20000. Notice that periodic
boundary conditions during the islands formation.

## Structure of the Lattice

The lattice is a multidimensional grid. We store it in a one
dimensional array, which means that we have to choose a convention.
The lattice is periodical, so we can imagine a torus for
a 2D lattice...

![Torus][torus]

...and so on...

![Torus 4D][torus4D]

Imagine the vector of spins wrapped on itself as many times as
the dimension of the problem.
Here, a 3D representation:

![3D Lattice][3dlat]

It's necessary to remember these assumptions when measuring quantities
such as energy on the lattice.

## Multidimensional Neighbour Interactions and Counting

Since the lattice is a mono dimensional `bool *` we need a method to
count the neighbours of each spin.

Here are examples of neighbour counting for mono dimensional and
bi dimensional lattice.

![1D Model][1Dmodel]

![2D model][2Dmodel]

Reduntant terms were omitted: `(i // N) * N` is zero when in max
dimension, also, `(i + 1) % N` `(i - 1 -N) % N` may be reduntant.

We can easily see a pattern. We use `i` as the index of the
spin in the lattice, `d` is a particular dimension where we
want to find the neighbours.
For a simple notation we used `//` and `**` in a python-ish style
meaning respectively integer division and power (power comes before
all the other operations).

```
(i // N**(d + 1))*N**(d + 1) + (i + N**d             ) % N**(d + 1)
(i // N**(d + 1))*N**(d + 1) + (i - N**d + N**(d + 1)) % N**(d + 1)
```
We can loop on `i` and `d` to obtain all the neighbours. The process
can be executed in parallel and be reduced with `if` statements on
the first and last iteration.

The first reduction is much more sensitive since let us to evaluate
a single power for each dimension > 1.


[1Dmodel]: img/1D.png "1D Model"
[2Dmodel]: img/2D.png "2D Model"
[cooling2D-1]: img/1-25.gif "Cooling of 2D Lattice"
[cooling2D-2]: img/2-25.gif "Cooling of 2D Lattice"
[cooling2D-3]: img/3-25.gif "Cooling of 2D Lattice"
[cooling2D-4]: img/4-25.gif "Cooling of 2D Lattice"
[3dlat]: img/structure.png "3D lattice structure"
[torus]: img/torus.png "Torus"
[torus4D]: img/torus4D.jpg "Torus in 4D"