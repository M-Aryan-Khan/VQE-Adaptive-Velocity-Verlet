# Adaptive Friction Velocity Verlet Optimization for VQE

[![Python](https://img.shields.io/badge/Python-3.7%2B-blue.svg)](https://www.python.org/)
[![Qulacs](https://img.shields.io/badge/Qulacs-Quantum%20Simulator-brightgreen.svg)](https://github.com/qulacs/qulacs)
[![PySCF](https://img.shields.io/badge/PySCF-Quantum%20Chemistry-orange.svg)](https://github.com/pyscf/pyscf)
[![SciPy](https://img.shields.io/badge/SciPy-latest-blue.svg)](https://www.scipy.org/)

This repository extends the research presented in the paper [Velocity Verlet-based optimization for variational quantum eigensolvers](https://arxiv.org/abs/2603.09862). 

While the original paper demonstrated the efficacy of classical physics-inspired optimizers (specifically Velocity Verlet) for the Variational Quantum Eigensolver (VQE), it relied on rigid, static hyperparameters. This project introduces a novel **Adaptive Velocity Verlet (AVV)** methodology to solve the issue of infinite energy oscillations and overshooting in rugged quantum landscapes.

## Key Contributions (Proposed Methodology)
* **Energy-Aware Dynamic Time-Stepping:** The algorithm actively monitors the energy landscape $\Delta E$. It shrinks the integration step size ($\Delta t$) upon detecting energy spikes to force localized exploration, and cautiously accelerates on flat, smooth terrain.
* **Exponential Momentum Decay:** Introduces an "emergency brake" (90% momentum decay) to prevent simulated particles from violently oscillating out of shallow local minima.
* **Gradient Caching:** Reuses analytical quantum gradients during braking events to vastly improve computational efficiency and reduce total quantum circuit evaluations.

## Compared Optimizers
The repository benchmarks the proposed AVV against the base paper and standard classical methods using Qulacs and PySCF statevector simulators on Hydrogen ($H_2$) and Lithium hydride (LiH) molecules:
- **Adaptive Velocity Verlet (Proposed)**
- Standard Velocity Verlet (Baseline)
- L-BFGS-B  
- SLSQP
- COBYLA  

## Results Overview
The Adaptive method successfully reduces the total number of required quantum circuit evaluations (e.g., saving ~1,000 evaluations on the 12-qubit LiH molecule). This improves computational efficiency and reduces susceptibility to hardware gate noise. However, it highlights a critical trade-off regarding absolute ground-state accuracy in highly rugged, high-dimensional parameter spaces. 

Full convergence plots, dynamic time-step graphs, and performance summary tables are available in the repository files.

## How to Run
This project was developed and tested in Google Colab to utilize fast cloud-based CPU simulation. 

1. Clone the repository:
   ```bash
   git clone [https://github.com/M-Aryan-Khan/VQE-Adaptive-Velocity-Verlet.git](https://github.com/M-Aryan-Khan/VQE-Adaptive-Velocity-Verlet.git)
Install the required quantum chemistry and simulation libraries:

2.
pip install qulacs pyscf openfermion openfermionpyscf
Execute the main script to run the benchmark:

3.
python main.py
