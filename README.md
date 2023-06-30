# Genetic Algorithm for Integrated Ramp Metering

This repository contains a genetic algorithm designed to solve the mixed integer optimization problem of Integrated Ramp Metering. The solution achieved closely mirrors the results produced by Gurobi's solver, demonstrating the flexibility and power of genetic algorithms for tackling complex optimization problems.

## Problem Statement

The core problem addressed is Integrated Ramp Metering. The mathematical formulation of the problem is as follows:

Objective Function:
**Maximize 𝑍 = 𝐷0 + Σ𝑋𝑗 (for 𝑗=1 to 4)**

Subject to Constraints:
1. **𝐷0𝐴0𝑗 + Σ𝐴𝑖𝑗𝑋𝑖𝑗 (for 𝑖=1) ≤ 𝐵𝑗 (for 𝑗=1 to 4)**
2. **𝑋𝑗 ≤ 𝐷𝑗**
3. **𝑋𝑗 ≥ 𝐷𝑗(1−𝑦𝑗)**
4. **𝑋𝑗 ≥ 𝑋𝑚𝑖𝑛𝑦𝑗**
5. **𝑋𝑗 ≤ 𝐷𝑗(1−𝑦𝑗) + 𝑋𝑚𝑎𝑥𝑦𝑗**
6. **𝑦𝑗 ≤ 𝑀𝑘𝑗**
7. **𝑋𝑗 − 𝐷𝑗 ≤ 𝑀(1−𝑘𝑗)**

Where:
* **𝑦𝑗** = {0 if No Ramp Metering, 1 if Ramp Metering}
* **𝑘𝑗**= 0 or 1
* **𝑋𝑚𝑎𝑥** and **𝑋𝑚𝑖𝑛** are set to 900 and 180, respectively.
* **𝑀** is considered a sufficiently large number. 

The goal of this problem is to find the optimal values of **𝑋𝑗**, **𝑦𝑗**, and **𝑘𝑗** that satisfy all constraints and maximize the objective function **𝑍**.

# Genetic Algorithm Approach for the Integrated Ramp Metering Problem

In the endeavor to solve the problem of Integrated Ramp Metering, we apply a Genetic Algorithm (GA) strategy. A GA is a heuristic inspired by the process of natural selection and it follows the principles of initialization, selection, crossover (or recombination), mutation, and termination. 

## Genetic Algorithm Description

The fundamental aspects of a Genetic Algorithm include:

1. **Initialization**: An initial population of potential solutions is randomly generated. These solutions are often binary-encoded as 0s and 1s, but can also be represented differently.

2. **Selection**: The most fit individuals are selected to transmit their traits to the next generation.

3. **Crossover**: This is the key phase in a GA. A crossover point within the gene is selected at random for each pair of parent solutions that are to be bred.

4. **Mutation**: In a few new offspring, certain genes may undergo mutation, which involves flipping some of the bits in the gene's encoding at a low, random probability.

5. **Termination**: The algorithm terminates when the population converges, i.e., it ceases to produce offspring that are significantly different from the previous generation. If the population hasn't converged, the algorithm goes back to the selection phase.

## Application of GA on the Problem

Here is the eight-step procedure applied to solve the problem with a Genetic Algorithm:

1. **Problem Encoding**: Our problem consists of four continuous variables x1 to x4, four binary variables y1 to y4, and four binary variables k1 to k4. We can represent these as a string of real numbers (for x) and binaries (for y and k) within a single individual.

2. **Population Initialization**: We generate a population of such strings, with the values randomized within the permissible range for each variable.

3. **Fitness Function Definition**: This function ranks the solutions. In our case, we aim to maximize Z, thus better solutions should yield higher function values.

4. **Selection**: Pairs of these solutions are selected for breeding. The selection is typically random, but with a higher preference for solutions with better fitness.

5. **Crossover**: For each pair, two offspring are created by swapping parts of the parents' encodings. The swapping can be at a single or multiple random points, keeping in mind the type preservation of each string part.

6. **Mutation**: In this step, a random part of the encoding in each offspring is altered. For y and k variables, a bit flip might be applied, whereas for x variables, a small random value could be added.

7. **Generation Evolution and Repetition**: Some or all of the old population is replaced by the new offspring, and the process is repeated from the selection step. The iteration continues until a predefined fitness criterion is met or after a certain number of generations.

8. **Evaluation**: Finally, the algorithm is evaluated to check if a termination condition (optimal or near-optimal solution discovery, or passage of a certain number of generations) has been met. If not, the algorithm cycles back to the selection step.
