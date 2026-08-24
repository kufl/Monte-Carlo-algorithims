# Monte Carlo Algorithms
This repository contains various Monte Carlo methods for computational chemistry, separated into branches. 

For starters, we have the two basic algorithms:
1. Direct Sampling (DMC)
2. Markov Chain Sampling (MCMC): Metropolis algorithm

The DMC algorithm can be regarded as many independent series of events occurring, while the MCMC algorithm utilises chains of events occurring dependent on the previous event.

This allows for different optimisation strategies, especially by utilising NumPy's vectorisation.
