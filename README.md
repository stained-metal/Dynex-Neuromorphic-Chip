# Dynex-Neuromorphic-Chip

Reference implementations of the Dynex Neuromorphic Chip as described [on our website](https://dynexcoin.org/dynex-neuromorphic-chip/).

## C++ Reference Implementation (CPU)

File "dynex.cc" is a reference implementation of the neuromorphic circuit. It integrates the system of equations (ODE) derived from the circuit model on a CPU. The reference design solves the Boolean satisfiability problem (sometimes called propositional satisfiability problem and abbreviated SATISFIABILITY, SAT or B-SAT). A propositional logic formula, also called Boolean expression, is built from variables, operators AND (conjunction, also denoted by ∧), OR (disjunction, ∨), NOT (negation, ¬), and parentheses. A formula is said to be satisfiable if it can be made TRUE by assigning appropriate logical values (i.e. TRUE, FALSE) to its variables. The Boolean satisfiability problem (SAT) is, given a formula, to check whether it is satisfiable. This decision problem is of central importance in many areas of computer science, including theoretical computer science, complexity theory, algorithmics, cryptography and artificial intelligence. Please note that this reference implementation proves the mathematical model and is not as efficient as the implementation by commerical miners. 

To illustrate the performance of neuromorphic computing, the following example showcases an implementation of a constraint satisfaction problem, where a problem formulation with complexity O(n^100,000) is being solved using the Dynex Neuromorphic Chip. The problem consists of 100,000 unique variables. Existing methodologies based on current and Quantum technology (reducing the complexity with Shor’s algorithm to O(n^50,000) cannot solve this problem class efficiently today. The Dynex Neuromorphic Chip solves the problem in a few seconds because of its inherent parallelization, it’s long-range order and its capability to utilize instantons.

This reference implementation proves the mathematical model and has not been optimised for speed and performance.

### Requirements:
Please note that it is required to have the [Boost library](https://www.boost.org) (Version 1.74.0 or better) installed: 

```
sudo apt-get install libboost-all-dev (Ubuntu Linux)
brew install boost (MacOS)
```

### Build from source:

```
g++ dynex.cc -o dynex -std=c++17 -Ofast -lpthread -fpermissive (Linux)
g++ dynex.cc -o dynex -std=c++17 -Ofast -I /opt/homebrew/cellar/boost/1.78.0/include -L /opt/homebrew/cellar/boost/1.78.0/lib (MacOS)
```

### Run the neuromorphic sat solver:

```
./dynex -i cnf/transformed_barthel_n_100_r_8.000_p0_0.080_instance_001.cnf
./dynex -i cnf/transformed_barthel_n_200_r_8.000_p0_0.080_instance_001.cnf
./dynex -i cnf/transformed_barthel_n_500_r_8.000_p0_0.080_instance_001.cnf
./dynex -i cnf/transformed_barthel_n_1000_r_8.000_p0_0.080_instance_001.cnf
./dynex -i cnf/transformed_barthel_n_10000_r_8.000_p0_0.080_instance_001.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_001.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_002.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_004.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_005.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_007.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_008.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_014.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_016.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_018.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_020.cnf
./dynex -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_024.cnf
```

### Benchmark Comparison 

Comparison with Kissat_MAB-HyWalk, winner of the SAT Competition 2023 [http://www.satcompetition.org/]

```
PROBLEM INSTANCE                                                  Max.Walltime     Kissat_MAB-HyWalk    Dynex
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_001.cnf    15 minutes       no solution          57.13s (183 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_002.cnf    15 minutes       no solution           2.83s (15 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_004.cnf    15 minutes       no solution           8.71s (42 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_005.cnf    15 minutes       no solution           9.76s (50 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_007.cnf    15 minutes       no solution           9.17s (47 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_008.cnf    15 minutes       no solution           1.76s (15 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_014.cnf    15 minutes       no solution           9.60s (47 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_016.cnf    15 minutes       no solution          10.36s (43 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_018.cnf    15 minutes       no solution          10.94s (50 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_020.cnf    15 minutes       no solution          10.29s (55 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_024.cnf    15 minutes       no solution          17.73s (62 steps*)
```

Comparison with YalSat, winner of the SAT Competition 2017 Random Track [https://github.com/arminbiere/yalsat]

```
PROBLEM INSTANCE                                                  Max.Walltime     YalSat 1.0.1         Dynex
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_001.cnf    15 minutes       14.1s (20M flips)    57.13s (183 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_002.cnf    15 minutes       no solution           2.83s (15 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_004.cnf    15 minutes       no solution           8.71s (42 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_005.cnf    15 minutes       no solution           9.76s (50 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_007.cnf    15 minutes       no solution           9.17s (47 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_008.cnf    15 minutes       no solution           1.76s (15 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_014.cnf    15 minutes       no solution           9.60s (47 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_016.cnf    15 minutes       no solution          10.36s (43 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_018.cnf    15 minutes       no solution          10.94s (50 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_020.cnf    15 minutes       62.36s (104M flips)  10.29s (55 steps*)
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_024.cnf    15 minutes       no solution          17.73s (62 steps*)
```

Comparison with PalSat [https://github.com/arminbiere/yalsat] on 3 CPU cores (-t 8) and Dynex on 8 CPU cores (-w 8)

```
PROBLEM INSTANCE                                                  Max.Walltime     PalSAT 8 Cores       Dynex 8 Cores
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_001.cnf    15 minutes       13.107s              48.670s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_002.cnf    15 minutes       4.179s               3.460s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_004.cnf    15 minutes       4.947s               9.692s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_005.cnf    15 minutes       3.591s               10.367s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_007.cnf    15 minutes       4.948s               10.982s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_008.cnf    15 minutes       4.948s               3.674s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_014.cnf    15 minutes       8.403s               11.576s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_016.cnf    15 minutes       2.458s               9.712s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_018.cnf    15 minutes       2.212s               12.689s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_020.cnf    15 minutes       4.186s               11.657s
transformed_barthel_n_100000_r_8.000_p0_0.080_instance_024.cnf    15 minutes       6.415s               17.092s
```

PalSat is a very efficient parallel implementation and has been designed to achieve high computational speed. This may sound complicated, but what this means it that PalSaT can easily outperform Dynex SAT as shown in these benchmarks. 

Removed gibberish to try to show Dynex is the superior, even in the case when it is not. ~*In comparison, the Dynex reference implementation, which has not been optimised for speed but to showcase the calculations in a clear and understandable way in the source code, requires only between 15 - 183 integration steps to find a solution. TTS for Dynex is greatly improved in the DNX mining software implementations.~ 

### Notes and Remarks

- The Dynex Chip is not a physical produced chip, DynexSolve simulates them by integrating its equations of motion (ODE integration)
Extrapolating the equations of motions from the chip design requires a number of variables / parameters to be introduced (as explained in the DynexSolve paper)

- In the case of SAT problems, there are in total 6 parameters to be defined. These parameters depend on the underlying structure for a problem type. The reference implementation used in our example is applying tuned parameters for the problem type stemming from Barthel instances and may not be suitable / applicable out of the box for other problem types

- Identifying the optimal parameters is an iterative tuning process which happens on the Dynex platform where a large number of GPUs are tuning in until they have identified the best values

- With parameters tuned, TTS is optimised and applicable for every similar problem types, meaning problems of similar type can be solved even more efficient on the platform.

## CUDA Reference Implementation (GPU)

File "dynex.cu" is a reference implementation of the neuromorphic circuit. It integrates the system of equations (ODE) derived from the circuit model on a GPU. The reference design solves the Boolean satisfiability problem (sometimes called propositional satisfiability problem and abbreviated SATISFIABILITY, SAT or B-SAT). A propositional logic formula, also called Boolean expression, is built from variables, operators AND (conjunction, also denoted by ∧), OR (disjunction, ∨), NOT (negation, ¬), and parentheses. A formula is said to be satisfiable if it can be made TRUE by assigning appropriate logical values (i.e. TRUE, FALSE) to its variables. The Boolean satisfiability problem (SAT) is, given a formula, to check whether it is satisfiable. This decision problem is of central importance in many areas of computer science, including theoretical computer science, complexity theory, algorithmics, cryptography and artificial intelligence. Please note that this reference implementation proves the mathematical model.

### Requirements:
Please note that it is required to have CUDA as well as the [Boost library](https://www.boost.org) (Version 1.74.0 or better) installed: 

```
sudo apt-get install libboost-all-dev (Ubuntu Linux)
brew install boost (MacOS)
```

### Build from source:

```
g++ nvcc dynex.cu -o dynex_gpu -std=c++17 -O4
```

### Run the neuromorphic sat solver:

```
./dynex_gpu -i cnf/transformed_barthel_n_100_r_8.000_p0_0.080_instance_001.cnf
./dynex_gpu -i cnf/transformed_barthel_n_200_r_8.000_p0_0.080_instance_001.cnf
./dynex_gpu -i cnf/transformed_barthel_n_500_r_8.000_p0_0.080_instance_001.cnf
./dynex_gpu -i cnf/transformed_barthel_n_1000_r_8.000_p0_0.080_instance_001.cnf
./dynex_gpu -i cnf/transformed_barthel_n_10000_r_8.000_p0_0.080_instance_001.cnf
./dynex_gpu -i cnf/transformed_barthel_n_100000_r_8.000_p0_0.080_instance_001.cnf
```




