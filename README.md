



# Economic Dispatch Optimization with Hopfield Neural Networks

**Apache 2.0 license** so attribution would be lovely, please and thank you.
Welcome to the repository for Economic Dispatch using Hopfield Neural Networks. This project focuses on solving the economic dispatch problem in power systems through a novel implementation of Hopfield Neural Networks (HNNs) tailored for multi-timestep optimization.

## Overview

**Economic Dispatch (ED)** is the process of allocating power generation among available units to meet demand at the lowest possible cost. The challenge is encapsulated by:

$$
\text{Minimize } \quad F = \sum_{i=1}^{N} (a_i + b_i P_i + c_i P_i^2)
$$

subject to:

- **Power Balance Constraint:**\
  $$\sum_{i=1}^{N} P_i - P^D - P^L = 0$$\
  where $(P^D)$ is the demand, $(P^L)$ represents transmission losses, typically modeled as:\
  \$$P^L = \sum_{i=1}^{N} B_i P_i^2$$
- **Capacity Constraints:**\
  $$P_{\text{min}, i} \leq P_i \leq P_{\text{max}, i} \quad \forall i = 1, \ldots, N$$

Here, $(N)$ is the number of generators, $(P_i)$ is the power output, and $(a_i, b_i, c_i)$ are cost coefficients. $(B_i)$ are the coefficients for transmission losses.

## Background

This project extends the work on Hopfield Neural Networks for optimization, particularly inspired by:

1. **Yalcinoz and Short (1997)** - "Large Scale Economic Dispatch Using an Improved Hopfield Neural Network"
2. **Yalcinoz, Short, and Cory (2001)** - "Hopfield Neural Network Approaches to Economic Dispatch Problems"

These papers focus on using HNNs for large-scale systems, managing constraints through modified activation functions and introducing new mapping techniques.

## Features of This Implementation

- **Multi-Timestep Optimization:** Considers temporal dynamics of demand over a 24-hour period in 30-minute increments.
- **Dynamic Weight Matrix:** Incorporates temporal coherence to link generator outputs across time.
- **Advanced Gradient Calculation:** Combines cost and constraint gradients for more accurate optimization:
  - **Cost Gradient:** Derived from the Hopfield network's energy function.
  - **Constraint Gradient:** Ensures demand is met across all timesteps.
- **Adaptive Learning Rate:** Dynamically adjusts for better convergence.
- **Data Generation:** Utilizes real-world data from Ireland to simulate realistic scenarios, including:
  - **Generator Capacities:** Based on observed data with added variability.
  - **Cost Coefficients:** Simulates different generator efficiencies.
  - **Transmission Losses:** Randomly generated to represent real-world complexities.
  - **Demand Profile:** Scaled to match the simulated system's capacity.

## Code Structure

### DataGenerator Class

- **Purpose:** Generates synthetic data for economic dispatch simulations.
- **Key Methods:**
  - `__init__`: Sets up generator characteristics and demand profiles.
  - `plot_demand_profile`: Visualizes the demand profile against total capacity.
  - `print_stats`: Outputs statistical information about the simulated system.

### HopfieldEconomicDispatch Class

- **Purpose:** Implements the Hopfield Neural Network for economic dispatch.
- **Key Methods:**
  - `__init__`: Initializes the network with given parameters.
  - `solve`: Runs the optimization to find generator outputs.
  - `step`: Performs one iteration of the optimization process.
  - `gradient_check`: Verifies the correctness of gradient calculations.
  - `calculate_dt`: Calculates the adaptive learning rate.

## Running the Code

This notebook was developed using Google Colab, plain vanilla free tier cpu only environment, if you are running locally you may need to diddle your library versions. You shouldn't need a GPU to complete an optimisation run in a reasonable timeframe.

## To Do
- Implement features to enable multi experiment runs
- Better instrumentation and analytic tools, especially for run comparisons
- Adapt calculate_dt to implement Ranger Hybrid Optimiser, prior to introducing more complexity
- Generator warmup / ramp rates
- Generator cooloff
- Dialable timesteps. Presently its fixed at 30 minutes. 15 and 5 minute intervals would be useful for warmup, ramp and cooloff.
- Kron's loss formula (Where transmission losses depend on both the output of the current generator and the output of every other generator on the same power bus)
