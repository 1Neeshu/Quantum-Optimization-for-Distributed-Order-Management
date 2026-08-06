project
Quantum Optimization for Distributed Order Management
Quantum-Classical Hybrid Optimization for DOM

A Python project that uses a Variational Quantum Eigensolver (VQE) with Pauli correlation encoding and a classical Mixed-Integer Linear Program (MILP) recourse to solve Distributed Order Management (DOM) routing problems.
Pauli Correlation Encoding scheme is particularly useful for problems with a large number of binary variables, as it allows the problem to be executed on current quantum computers, which have a limited number of available qubits (e.g., compressing 8 routing decisions into just 3 physical qubits).

Features
DOM Problem Mapping: Reads logistics data, inventory, and capacity constraints from CSV files and maps the contested supply chain routing choices to a quantum circuit.

Pauli Correlation Encoding (PCE): Implements a specific encoding scheme to represent binary keep-or-divert variables using Pauli operators.

Hybrid VQE-MILP Algorithm: Utilizes a hybrid quantum-classical approach to find the optimal assignment, combining continuous quantum parameter updates with exact classical MILP feasibility checks.

Flexible Simulation: Supports running the algorithm on an exact simulator, a shot-based simulator, or a noisy simulator that models a real backend.

Hardware-Efficient Ansatz: Includes support for quantum circuits like EfficientSU2 to serve as the ansatz for the VQE.

Classical Optimization: Employs classical optimizers like COBYLA with an Augmented Lagrangian loss function to find the optimal parameters for the ansatz circuit.

1. **Clone the repository:**
```bash
git clone https://github.com/your-username/quantum-dom-optimization.git
cd quantum-dom-optimization

```


2. **Create a virtual environment** (recommended):
```bash
cd project
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

```


if conda:
```
conda create --name project_name
conda activate project_name

```


3. **Install dependencies:**
```bash
pip install -r requirements.txt

```


For conda packages can be installed one by one, some may not be available on conda channel

Usage
Set up IBM Quantum Credentials:
The script can run on a noisy simulator based on a real IBM Quantum device. To do this, you need to provide your IBM Quantum API token and CRN (Cloud Resource Name).

Find your credentials: Log in to your IBM Quantum account. Go to your dashboard to find your API token and the CRN for your preferred instance

Update run.py:
Open run.py and replace the placeholder values for my_token and my_instance with your actual credentials.
Warning: Do not commit your personal tokens to a public repository. If you are not using a real backend simulation, you can leave these as placeholders.
Choose a Simulation Type:
The execution flow uses a simulation configuration to determine the execution environment. You can modify this in run.py to select the desired simulation.

'exact': Runs on an AerSimulator (or AerEstimator) using the statevector method. This provides the most precise results but is limited to a small number of qubits due to memory constraints.

'shot_based': Runs on an AerSimulator that uses a finite number of measurement shots. This simulates a real quantum computer's measurement process, introducing statistical noise.

'noisy_shot_based': Runs on an AerSimulator that incorporates a custom noise model (like FakeManilaV2). This allows for a more realistic simulation of a quantum device's behavior.

'Noisy_backend_real': This option is designed for advanced use cases where a real IBM Quantum backend is used to generate the noise model for a local simulation. It requires a token and instance to access the backend's calibration data.

Execute the run.py file from the root directory of the repository.
The script will begin the VQE optimization, printing the cost and constraint violations at each iteration. It will then output the final benchmark cost of the solution found, apply a classical 1-bit neighborhood repair, and save the final planner recommendations.
