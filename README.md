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
