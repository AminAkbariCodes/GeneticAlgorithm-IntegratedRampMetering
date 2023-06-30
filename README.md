# Genetic Algorithm for Integrated Ramp Metering

This repository contains a genetic algorithm designed to solve the mixed integer optimization problem of Integrated Ramp Metering. The solution achieved closely mirrors the results produced by Gurobi's solver, demonstrating the flexibility and power of genetic algorithms for tackling complex optimization problems.

## Problem Statement

The core problem addressed is Integrated Ramp Metering. The mathematical formulation of the problem is as follows:

Objective Function:

\[
\max Z = D_0 + \sum_{j=1}^{4}X_j
\]


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

## Requirements

- Python 3.x+
- pandas
- numpy
- gurobipy
- copy
- time

## Code Structure
### Genetic Algorithm
The Genetic Algorithm (GA) implementation consists of the following parts:

- `create_individual(bounds)`: Create a single individual (solution).
- `create_population(bounds, size)`: Create a population of individuals.
- `calculate_fitness(individual, Aij, Demand, Capacity, M=1000000000)`: Calculate the fitness of an individual solution.
- `roulette_wheel_selection(population, fitnesses)`: Select individuals for breeding.
- `tournament_selection(population, fitnesses, tournament_size)`: An alternative selection method.
- `single_point_crossover(parent1, parent2)`: Generate two offspring from two parents.
- `mutation(individual, mutation_rate, mutation_strength=0.1)`: Mutate an individual.
- `create_new_generation(population, Aij, Demand, Capacity, mutation_rate, M=10000000000)`: Create a new generation of solutions.
- `genetic_algorithm(Aij, Demand, Capacity, mutation_rate, num_generations, population_size)`: The main GA function, which brings together all the steps.

Running the GA and printing the results.

### Gurobi
The Gurobi implementation has the following parts:

- Input the data from an Excel file using pandas.
- Create a model using Gurobi.
- Define decision variables.
- Set the objective function.
- Add constraints.
- Optimize the model using Gurobi.
- Print the results.

## File Structure
The project consists of two Jupyter Notebook files (`Genetic-Algorithm.ipynb` and `Gurobi.ipynb`), and one Excel data file (`data.xlsx`). The data file includes the following sheets: `Aij`, `Demand`, and `Capacity`, which provide input data for both the GA and Gurobi solutions.

## Results
The results obtained from the Gurobi solution and the GA solution are displayed in the notebooks. The GA solution's fitness is compared with the Gurobi solution's fitness to estimate the accuracy of the GA implementation. The notebooks also include a calculation of the Mean Absolute Percentage Error in the solutions.

The solutions obtained after running the GA and Gurobi are as follows:

#### Genetic Algorithm Results
- Parameters: `mutation_rate=0.1`, `num_generations=1000`, `population_size=100`
- Best solution: `[330.98950416425885, 181.75237603751017, 460.0, 1000.0, 1, 1, 1, 0, 1, 1, 1, 1]`
- Fitness of the best solution: `6572.741880201769`
- Runtime(min): `0.8691247383753459`

#### Gurobi Results
- Solution: `[333.333, 180, 460, 1000, 1, 1, 0, 0, 1, 1, 0, 0]`
- Fitness value of the Gurobi solution: `6573.3330000000005`

#### Error Metrics
- Relative Error in Fitness (%): `0.008992695155279295`
- Mean Absolute Percentage Error in Solution Values (%): `0.419147924020311`

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)
