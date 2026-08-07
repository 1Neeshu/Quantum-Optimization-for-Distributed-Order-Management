# Quantum Optimization for Distributed Order Management (DOM)

**Team:** The Quantum DOMinators  
* Authors: Neeshu Rathi (neeshu_r@ma.iitr.ac.in) & Shiplu Sarker (shiplu1983@gmail.com)  
* Program: WISER x Nestlé Global Quantum+AI Program 2026

A Python project applying a Variational Quantum Algorithm with Pauli Correlation Encoding (PCE) alongside a classical Mixed-Integer Linear Program (MILP) recourse to solve Distributed Order Management routing problems.

The Pauli Correlation Encoding scheme allows large numbers of binary variables to be executed on near-term quantum hardware with limited qubits by compressing multi-variable supply chain decisions into fewer physical qubits.

## Features
* DOM Problem Mapping: Reads logistics data, inventory, and capacity constraints from CSV files to map supply chain routing choices to a quantum circuit.
* Pauli Correlation Encoding (PCE): Implements an encoding scheme representing binary keep-or-divert variables using multi-body Pauli operators.
* Hybrid Quantum-Classical Algorithm: Combines continuous quantum parameter updates via COBYLA with exact classical MILP feasibility checks using an Augmented Lagrangian loss function.
* Hardware-Efficient Ansatz: Utilizes quantum circuits like efficient_su2 as the variational training ansatz.
* Automated Noisy Simulation: Benchmarks trained quantum models against ideal statevectors and evaluates noise resilience using real backend snapshots like IBM's FakeManilaV2.

## Data Setup and Privacy Note
Due to WISER and Nestlé data privacy restrictions, raw operational datasets must not be published outside the authorized environment. 

To run optimization scripts locally:
1. Download the anonymized POC data pack from the official WISER Challenge Google Drive ([https://drive.google.com/drive/folders/1LmlL5BiPcbcdl1aRhPaAEGm40m1PNvM5](https://drive.google.com/drive/folders/1LmlL5BiPcbcdI1aRhPaAEGm40m1PNvM5)).
2. Extract the CSV files anywhere inside this project folder. The built-in locate_csv function automatically scans and loads them.
3. Execute the script following the instructions below.

## Setup and Installation
2. Create a virtual environment (recommended):

Using standard venv (macOS/Linux):

```bash
python3 -m venv venv
source venv/bin/activate

```

Using standard venv (Windows):

```bash
python -m venv venv
venv\Scripts\activate

```

Using Conda:

```bash
conda create --name dom_quantum python=3.10
conda activate dom_quantum

```

3. Install dependencies:

```bash
pip install -r requirements.txt

```

## Usage

Execute the main script from the root directory:
python run.py

### Execution Flow
Local fake backends simulate noise, meaning no IBM Quantum API token or cloud credentials are required. The script automatically executes the following steps:
1. Classical Benchmarking: Runs Default, Greedy, and Exact solvers to establish performance baselines.
2. Hybrid Training: Executes VQE optimization using COBYLA, logging costs, constraint violations, and Augmented Lagrangian multipliers.
3. Noise Analysis: Runs 20 noisy trials using a real IBM backend snapshot (FakeManilaV2) with 4096 shots to measure hardware resilience.
4. Post-Processing: Applies classical 1-bit neighborhood repairs to recover optimal states from noisy hardware distributions.

### Outputs
Upon completion, the script generates several diagnostic and business metric files:
* hybrid_order_recommendations.csv
* method_comparison.csv
* pce_variable_mapping.csv
* pce_diagnostics.csv
* pce_optimization_history.csv
* postprocessing_trace.csv
* noise_diagnostics.csv
* noise_trials.csv
* scaling_analysis.csv
* submission_readiness.csv
* hybrid_line_level_allocation.csv

### Credits & Acknowledgments
* Challenge Organizers: WISER Institute & Nestlé Global Quantum+AI Program 2026.
* Libraries: Developed using Python, PuLP (CBC), SciPy (COBYLA), Qiskit, and Qiskit Aer.
