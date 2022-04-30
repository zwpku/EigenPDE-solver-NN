# EigenPDE-NN
An Eigenvalue PDE Solver by Neural Networks

This package trains artificial neural networks to solve the first several eigenvalues/eigenfunctions of the eigenvalue PDE problem 
<img src="https://render.githubusercontent.com/render/math?math=-\mathcal{L}f=\lambda f">, where ![formula](https://render.githubusercontent.com/render/math?math=\mathcal{L}) is the infiniesimal generator of certain type of stochastic diffusion processes whose invariant measure is ![formula](https://render.githubusercontent.com/render/math?math=\mu).

A trajectory data (possibly biased with biasing weights) is needed as training data. Such data can be generated either 
- using a numerical scheme (e.g., Euler-Maruyama scheme), for diffusion processes whose stochastic differential equation (SDE) is <img src="https://render.githubusercontent.com/render/math?math=dX_t = -\nabla V(X_t)dt%2b\sqrt{2\beta^{-1}}dW_t"> with a relatively simple potential <img src="https://render.githubusercontent.com/render/math?math=V">; or 
- using a molecular simulation package (e.g., NAMD), for molecular systems.

## Preparation
#### 1. Dependances 

- [PyTorch](https://pytorch.org/)

- [MDAnalysis](https://www.mdanalysis.org/) is used to load MD data. 

- [slepc4py](https://pypi.org/project/slepc4py/) and [petsc4py](https://pypi.org/project/petsc4py/) are used in solving 2D eigenvalue PDE problems using finite volume method. In some examples, the solution given by finite volume method can be used to compare with the neural network solution. 
These two packages are not needed if one only wants to solve a PDE problem by training neural networks.

#### 2. Download the code 

```
	git clone https://github.com/zwpku/EigenPDE-NN.git
```

## Two examples 
Two examples are included under [./examples](examples).

### Example 1: A 50-dimensional system 

The potential in this example has 3 metastable regions. The training data can be 
generated directly by sampling the system's SDE using Euler-Maruyama scheme.

Steps to solve the eigenvalue PDE:

#### 1. Enter the directory corresponding to this example

```
    cd ./EigenPDE-NN
    cd ./examples/test-ex1-50d
```

#### 2. Generate trajectory data

  Run the script [main.py](examples/test-ex1-50d/main.py) by `python ./main.py`, and choose task 0 from input.

#### 3. Train neural networks

  Run the script [main.py](examples/test-ex1-50d/main.py) by `python ./main.py`, and choose task 3 from input.

### Example 2: Alanine Dipeptide example 

In this example we solve the eigenvalue PDE of the simple molecular system called alanine dipeptide in vacuum.  The training data is generated using the molecular simulation package NAMD. To overcome the sampling difficulties due to the strong metastability of the system, adaptive biasing force (ABF) method is used with the system's two dihedral angles as collective variables.

Steps to solve the eigenvalue PDE:

#### 1. Enter the directory corresponding to this example

```
    cd ./EigenPDE-NN
    cd ./examples/test-ex2
```

#### 2. Generate MD data
  Follow the steps in [README](examples/test-ex2/MDdata/README.md).

#### 3. Prepare data for training 
  Run the script [main.py](examples/test-ex2/main.py) by `python ./main.py`, and choose task 0 from input.

#### 4. Train neural networks

  Run the script [main.py](examples/test-ex2/main.py) by `python ./main.py`, and choose task 3 from input.
