# Random Walk Model of Motor Protein Transport in a Ratchet Potential

Simulation of motor protein motion (such as myosin) modeled as particles undergoing 
biased random walks in switching, ratchet potentials. A simplified 
theoretical model for how motor proteins convert chemical energy (ATP) into mechanical energy.

## Background

Motor proteins can't rely on a constant force to move directionally, since thermal 
fluctuations dominate at the molecular scale. Instead, they exploit an asymmetric, 
switching potential landscape: particles diffuse freely in one energy level, then 
relax into a sawtooth-shaped ("ratchet") potential in the other. Because the 
potential is asymmetric, this produces a net particle current — even though 
individual steps are random.

This project implements that model from scratch:
- Derives the correspondence between discrete random walks and the diffusion 
  equation
- Implements a Metropolis-like random walk where step probabilities depend on 
  the local potential gradient and temperature
- Simulates particles switching between a periodic sawtooth potential V₁(x) 
  and a flat potential V₂(x) at fixed intervals
- Compares simulated particle current against an analytical solution derived 
  from the diffusion equation

## Method

- **Random walk with biased transition probabilities**: at each step, a particle 
  moves left/right/stays based on Boltzmann-weighted probabilities from the local 
  potential
- **Periodic switching**: particles alternate between the sawtooth potential 
  V₁(x) and flat potential V₂(x) every `Tp` time steps, simulating the ATP-driven 
  excitation/de-excitation cycle
- **Current calculation**: net particle current computed as the difference 
  between rightward and leftward moves per cycle, normalized by particle count
- **Validation**: numerical results compared against an analytical expression 
  for cycle-averaged current (derived via the error function) in the limit of 
  fast diffusion

## Key results

- The particle current's direction is controlled by alpha, the parameter controlling the shape of the sawtooth potential.
  At alpha=0.5 the sawtooth is balanced and we get near 0 current.
- For longer periodic time intervals, where particles are allowed to live in each landscape V1, V2 for longer times,
  the numerical and analytic solution are similar. For short time periods Tp, the solutions diverge.

## Tools

Python, NumPy, SciPy (curve fitting, error function), Matplotlib

---
*Project for TMA4230 "Vitenskapelige Beregninger" / biophysics assignment, NTNU, 2025. 
Based on an assignment by Johanne B. Tjernshaugen, NTNU.*
