## Summary of Lecture Notes on Vector/Matrix Calculus and Lagrange Multipliers for 3D Computer Vision

These lecture notes cover essential mathematical tools for 3D computer vision. The first part focuses on vector and matrix calculus, including notation, derivatives of scalar functions with respect to vectors (specifically L2 norm, scalar product, and vector-matrix-vector product), and the application of these concepts to solving overdetermined linear systems using the least-squares method. It demonstrates how to apply this to line and plane fitting. The second part introduces Lagrange multipliers as a technique for solving constrained optimization problems. It explains the underlying principle of parallel gradients and demonstrates its application in finding optimal solutions, particularly for homogeneous linear systems and in computer vision tasks like plane fitting and determining the distance from a point to a line/plane. Finally, Singular Value Decomposition (SVD) is introduced as a fundamental matrix factorization technique.

## Detailed Explanation of Lecture Notes

### 1. Vector and Matrix Calculus for 3D Computer Vision

**1.1 Notation:**

The notes begin by establishing standard notation: bold fonts for matrices and vectors, column vector representation by default, and superscript 'T' for transpose to represent row vectors. Matrices are denoted by capital letters.

**1.2 Derivatives:**

The core of the first lecture note revolves around the definition of the derivative of a scalar function *J* with respect to a vector **x**. This derivative,  ∂*J*/∂**x**, is a column vector containing the partial derivatives of *J* with respect to each element of **x**.

**1.2.1 Notable Derivatives:**

*   **L2 norm of a vector:** The derivative of the L2 norm squared of a vector **x** (||**x**||² = **x**<sup>T</sup>**x**) with respect to **x** is derived to be 2**x**. The proof involves expanding the norm as a sum of squares and taking the partial derivative with respect to each element of **x**.

*   **Scalar product of two vectors:** The derivative of the scalar product of two vectors **x** and **a** (**x**<sup>T</sup>**a**) with respect to **x** is shown to be **a**. This utilizes the commutativity of the scalar product.

*   **Vector-matrix-vector product:**  The derivative of a scalar function *J* = **x**<sup>T</sup>**A** **x** (where **A** is a matrix) with respect to **x** is derived as (**A**<sup>T</sup> + **A**) **x**. The derivation involves expanding the quadratic form and taking partial derivatives. A special case is highlighted where if **B** is a symmetric matrix (**B**<sup>T</sup> = **B**), then the derivative of **x**<sup>T</sup>**B** **x** is 2**B** **x**.

**1.3 Inhomogeneous Over-determined Linear Systems:**

The lecture then addresses how to solve systems of linear equations **A** **x** = **b** where there are more equations than unknowns (m > n). In such cases, a perfect solution may not exist, and the goal is to find an estimate for **x** that minimizes the difference between **A** **x** and **b**. This leads to the concept of the least-squares solution.

The objective is to minimize the squared L2 norm of the residual: ||**A** **x** - **b**||². By expanding this norm and taking the derivative with respect to **x**, setting it to zero, we arrive at the normal equation: **A**<sup>T</sup>**A** **x** = **A**<sup>T</sup>**b**. The solution for **x** is then given by **x** = (**A**<sup>T</sup>**A**)<sup>-1</sup>**A**<sup>T</sup>**b**.

**1.4 Case Studies:**

*   **Line fitting:** The least-squares method is applied to fitting a line *y* = *mx* + *b* to a set of 2D points. By formulating the problem as a system of linear equations and applying the least-squares solution, expressions for the optimal slope *m* and intercept *b* are derived.

*   **Plane fitting:**  Similarly, the method is extended to fitting a plane *z* = *ax* + *by* + *c* to a set of 3D points. A system of linear equations is formed, and the least-squares solution provides the optimal plane parameters *a*, *b*, and *c*.

### 2. Lagrange Multipliers

**2.1 Introduction:**

The second lecture note introduces Lagrange multipliers, a powerful technique for finding the extrema of a function subject to equality constraints. The goal is to solve constrained minimization/maximization problems.

**2.1.1 2D problem:**

The concept is initially illustrated with a 2D problem: minimizing a function *f*(*x*, *y*) subject to a constraint *g*(*x*, *y*) = *c*. The geometric intuition is that the minimum or maximum occurs when a level curve of *f* is tangent to the constraint curve *g*. At the point of tangency, the gradients of *f* and *g* are parallel.

**2.1.2 Applying a Lagrange multiplier in arbitrary dimensions:**

The method is generalized to arbitrary dimensions. A Lagrangian function *J* is formed by combining the objective function *f*(*x*) and the constraint *g*(*x*) = *c* using a Lagrange multiplier λ: *J* = *f*(*x*) - λ(*g*(*x*) - *c*).

To find the extrema, the partial derivatives of *J* with respect to **x** and λ are set to zero. Setting the derivative with respect to **x** to zero yields ∇*f* = λ∇*g*, confirming the parallel gradients condition. Setting the derivative with respect to λ to zero recovers the original constraint *g*(*x*) = *c*.

### 3. Application: Optimal Solution for a Homogeneous Linear System of Equations

Lagrange multipliers are then applied to find the optimal solution for a homogeneous linear system **A** **x** = 0, specifically seeking a non-trivial solution. The problem is formulated as minimizing the norm of **A** **x** subject to the constraint that the length of **x** is unity (**x**<sup>T</sup>**x** = 1).

The Lagrangian function is *J* = **x**<sup>T</sup>**A**<sup>T</sup>**A** **x** - λ(**x**<sup>T</sup>**x** - 1). Taking the derivative with respect to **x** and setting it to zero leads to **A**<sup>T</sup>**A** **x** = λ**x**. This is the eigenvalue equation, indicating that the optimal solution **x** is an eigenvector of **A**<sup>T</sup>**A**.

The value of the cost function at the optimum is equal to the eigenvalue λ. To minimize the norm, the eigenvector corresponding to the smallest eigenvalue of **A**<sup>T</sup>**A** is chosen. To maximize the norm, the eigenvector corresponding to the largest eigenvalue is chosen.

### 4. Application in Computer Vision: Plane Fitting

**4.1 Plane fitting:**

The notes revisit plane fitting, now using a homogeneous form *ax* + *by* + *cz* + *d* = 0. If points lie on the plane, substituting their coordinates yields a system of linear equations. The optimal solution for the parameters [a, b, c, d] is the eigenvector corresponding to the smallest eigenvalue of a specific matrix formed from the coordinates of the points.

**4.2 Application in geometry: optimal line/plane fitting:**

*   **Distance of a point and a line/plane:** Lagrange multipliers are used to find the distance between a point **x**<sub>0</sub> and a line/plane defined by **l**<sup>T</sup>**x** + *m* = 0. The problem is to minimize the squared distance ||**x** - **x**<sub>0</sub>||² subject to the constraint **l**<sup>T</sup>**x** + *m* = 0. The solution involves setting up the Lagrangian, taking derivatives, and solving for **x** and the Lagrange multiplier λ. The distance is then calculated.

*   **Optimal line/plane fitting:**
    *   **Translation:** To fit a line/plane to *N* data points, the optimal translation (offset) **t** is found by minimizing the sum of squared distances. This leads to the result that **t** is the negative of the mean of the data points.
    *   **Rotation:** After centering the data, the optimal orientation of the line/plane is determined by finding a unit vector **l** that minimizes the sum of squared distances from the points to the line/plane. This again leads to an eigenvalue problem, where the optimal **l** is the eigenvector corresponding to the smallest eigenvalue of a matrix formed from the centered data points.

### 5. Singular Value Decomposition

The first lecture note concludes with a brief introduction to Singular Value Decomposition (SVD). For any matrix **A**, SVD provides a factorization **A** = **U** **S** **V**<sup>T</sup>, where **U** and **V** are orthogonal matrices, and **S** is a diagonal matrix containing the singular values. The columns of **U** and **V** are the eigenvectors of **A** **A**<sup>T</sup> and **A**<sup>T</sup>**A**, respectively. The singular values are the square roots of the eigenvalues of these matrices. The singular values are typically arranged in descending order.

These lecture notes provide a solid foundation in vector and matrix calculus and optimization techniques crucial for understanding and implementing algorithms in 3D computer vision. The combination of basic derivative rules, least-squares methods, and the powerful tool of Lagrange multipliers equips students with the necessary mathematical background for various tasks like fitting geometric primitives and solving constrained optimization problems.
