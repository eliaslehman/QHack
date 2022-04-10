# Part 2 README

## General Overview

The quantum computing simulators provided by IBM and Quantinuum offer an emulated error to capture the noise and inconsistencies that arise in a physical quantum processor. However, IonQ doesn't offer such a feature. Therefore, we aim to implement a noise function $\xi(\rho)$ to provide users information on how accurate their IonQ simulations generally are. Afterwards, we aim to compare our results with an IonQ quantum processor to distinguish any differences with the simulation.

Gao and Duan (2018) discuss how for a density operator $\rho$, a generalized type of depolarized noise can be represented by the composition of Pauli errors $`\xi(\rho) = \xi_3{\circ}\xi_2{\circ}\xi_1`$, where $\xi_i = (1 - \epsilon_i)\rho + \epsilon_i\sigma_i\rho\sigma_i$ for i = 1,2,3 and $\sigma_1 = Z, \sigma_2 = X, \sigma_3 = Y$ (the Pauli gates). Thus, after composing the functions, the final noise function can be simplified as $\xi(\rho) = (1 - \epsilon_x - \epsilon_y - \epsilon_z)\rho + \epsilon_{X}X{\rho}X + \epsilon_{Y}Y{\rho}Y + \epsilon_{Z}Z{\rho}Z$. We define $\rho$ by a linear combination of Pauli Matrices with respect to our position on the Bloch Sphere for the entire circuit: $\rho = \frac{I + r_X{X} + r_Y{Y} + r_Z{Z}}{2}$. The depolarizd noise channel can also be written as $\xi(\rho) = (1 - \gamma)\rho + \frac{{\gamma}Tr[\rho]I}{2^n}$, where $\gamma$ is the depolarized error parameter, which is of the range $0 \le \gamma \le \frac{4^n}{4^n-1}$ (Qiskit). We take $\gamma$ to be the error value (akin to the standard deviation) for a uniformly distributed error in the channel.

## Running the Code

The code for our project is included in the Part 2 folder of this repository as a .ipynb notebook. To run the code, simply move the file to Microsoft Azure Quantum and run the file, as the code already predefines the different targets it wants to run on when executed.


## User Inputs

Users have full control over the type of Pauli circuits they want to test. Our project takes a custom quantum circuit and returns the estimated noise bound by running that circuit on an IonQ quantum computer. The components of the circuit must be within the Pauli group for our program program. To run the code, create a custom quantum circuit in the final cell and run all. For example, 
QC = QuantumCircuit(1, 1) 
qc.x(0)
qc.measure()
Will detail the error for a 1-qubit system with one Pauli X Gate. Running all will return the depolarized noise matrix and estimated error of the circuit $\gamma$.

*Note: This circuit must run on a non-ideal quantum simulator (error>0) or a quantum computer. Otherwise, there will me no errors in the gates and the code wont work.

