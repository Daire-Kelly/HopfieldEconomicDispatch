



# A Modern Approach to Hopfield Neural Networks and Economic Dispatch Optimisation
This repository offers a Python-based Hopfield Neural Network (HNN) solver for economic dispatch (ED) problems in power systems, building on the foundational work by T. Yalcinoz, M.J. Short, and B.J. Cory in their 2001 paper, "Hopfield Neural Network Approaches to Economic Dispatch Problems" (International Journal of Electrical Power & Energy Systems, Vol. 23, No. 6, pp. 435-442). It optimizes generator outputs to minimize fuel costs while meeting demand and constraints across a 48-timestep profile, using synthetic data inspired by Ireland's grid on January 31, 2025.
## Features
**Multi-Timestep Optimisation**: Extends the paper’s single-load approach to a full day’s demand cycle, enhanced with RAdam and Lookahead optimizers.
**Projected Gradient Enhancements**: Improves the paper’s projected gradient method with adaptive step sizes and modern optimization techniques for faster, more stable convergence.
**Dynamic Loss Handling**: Adjusts transmission losses iteratively across timesteps.
**Visual Insights**: Includes plots for energy, cost, and demand fulfillment.
**Scalability**: Tested on 40 units, designed to scale to larger systems (paper tested 3-240 units).
## License
Licensed under the Apache 2.0 License.
