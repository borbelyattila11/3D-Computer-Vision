# Basic Estimation Theory

## Inhomogeneous Linear System
In many 3D vision problems, we have an overdetermined system where $m > n$, meaning there are more equations than unknowns. In such cases, there is no exact solution that satisfies all equations, but we can find approximate solution using **least squares**.

$Ax = b$

Where:
- $A ∈ R^{m × n}$ is a matrix with $m$ equations and $n$ unknonws (variables)
- $x ∈ R^n$ is the vector of unknowns that we need to solve
- $b ∈ R^m$ is the vector of observations

## Homogeneous Linear Systems
The system $Ax = 0$ is called homogeneous because the right-hand side is the zero vector. The matrix $A$ is usually $m × n$, and $x$ is a vector of unknowns in $R^n$.

#### Non-Trivial Solution
In general, for a non-trivial solution $x != 0$ to exist, the matrix $A$ must be singular, meaning it has a determinant of zero, this means $A$ doesn't have a full rank (linear dependence). In an overdetermined system, where the number of equations exceeds the number of unknowns, the matrix $A$ is typically expected to be full rank.

If linear dependence exists the system no longer has a unique solution, and in fact, it will have infinitely many solutions. Dependence between the rows or columns of $A$ means that some of the equations in the system do not add any new information.

#### Eigenvalue Problem
Homogeneous linear systems $Ax = 0$ are closely related to the eigenvalue problem. Specifically, finding the non-trivial solutions is akin to finding the null space of $A$, which is equivivalent to solving for eigenvectors corresponding to the eigenvalue zero.
