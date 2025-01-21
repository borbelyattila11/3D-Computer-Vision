# Multi-View Reconstruction and Optimization Techniques in 3D Computer Vision

This document summarizes advanced methods for multi-view reconstruction in 3D computer vision, focusing on reconstruction strategies, optimization techniques, and their mathematical formulations.

---

## 1. Tomasi-Kanade Factorization
The Tomasi-Kanade factorization method is a linear approach for reconstructing 3D points using orthogonal or weak-perspective projections. Tracked 2D points across multiple views form a measurement matrix \( W \), which can be decomposed as:

\[
W = MS
\]

Where:
- \( M \): Camera motion matrix.
- \( S \): 3D structure matrix.

### Steps:
1. Use Singular Value Decomposition (SVD) to reduce \( W \) to rank 3, removing noise.
2. Enforce metric constraints to resolve affine ambiguities, ensuring that motion vectors are orthonormal.

For weak-perspective models:
- Vectors are constrained to have equal lengths but are not unit-length.
- Iterative optimization ensures convergence to a valid geometric reconstruction.

---

## 2. Reconstruction by Merging Stereo Reconstructions
Stereo reconstruction combines 3D point clouds from multiple calibrated image pairs.

### Calibration:
- **Intrinsic parameters**: Determined using techniques like Zhang's calibration (e.g., focal length).
- **Extrinsic parameters**: Derived from the essential matrix to define rotation and translation.

### Point Cloud Alignment:
To align point clouds, a similarity transformation is used:

\[
q_i = sR p_i + t
\]

Where:
- \( s \): Scale.
- \( R \): Rotation.
- \( t \): Translation.

### Optimization:
The goal is to minimize the alignment error:

\[
\sum ||q_i - (sR p_i + t)||^2
\]

Using Singular Value Decomposition (SVD), optimal transformations for rotation, scale, and translation are computed.

---

## 3. Numerical Optimization
Numerical optimization refines 3D reconstructions by minimizing reprojection errors.

### Objective:
Adjust 3D points and camera parameters to align projected 2D points with observed data.

### Method:
- **Algorithm**: Sparse Levenberg-Marquardt (LM) is used for efficiency in solving large-scale systems.
- **Jacobian Matrix**: Represents derivatives of the reprojection error with respect to all parameters, exploiting sparsity to reduce computational cost.


# Numerical Optimization

## Introduction
In 3D computer vision and other estimation tasks, many optimization problems lack closed-form solutions. These problems are often tackled using **numerical optimization techniques**, which iteratively minimize the cost function starting from an initial point.

---

## Approximation by Taylor Series
The cost function \( J(x) \) near \( x_0 \) can be approximated using a Taylor series:

\[
J(x_0 + \Delta x) = J(x_0) + \nabla J^T(x_0)\Delta x + \frac{1}{2}\Delta x^T H \Delta x + \dots
\]

- **Gradient** (\( \nabla J(x) \)): First derivatives of \( J(x) \).
- **Hessian Matrix** (\( H(x) \)): Second derivatives of \( J(x) \), symmetric due to mixed partial derivative equality.

---

## Optimization Methods

### 1. Gradient Descent
Moves in the direction of the steepest descent:
\[
\Delta x = -\alpha \nabla J
\]
where \( \alpha \) is a step size, typically tuned empirically.

### 2. Newton's Method
Uses second-order Taylor expansion, focusing on the quadratic terms:
\[
\Delta x = -H^{-1} \nabla J
\]
Efficient for problems where \( H \) is easily invertible.

### 3. Gauss-Newton Method
Designed for least-squares problems, where the cost function \( J \) is the sum of squared terms:
\[
J = \sum_{j=1}^M f_j^2(x)
\]
Gradient and Hessian approximations:
\[
\nabla J = 2 \nabla^T f(x) f(x), \quad H \approx 2 \nabla^T f(x) \nabla f(x)
\]
Iteration:
\[
\Delta x = -\left( \nabla^T f(x) \nabla f(x) \right)^{-1} \nabla^T f(x) f(x)
\]

---

## Levenberg-Marquardt Algorithm
Combines gradient and Gauss-Newton methods. The update step:
\[
\Delta x = \left( \nabla^T f(x) \nabla f(x) + \alpha I \right)^{-1} \nabla^T f(x) f(x)
\]
- \( \alpha = 0 \): Gauss-Newton method.
- \( \alpha \) large: Gradient descent dominates.

---

Numerical optimization is a powerful tool for solving complex problems iteratively, leveraging gradients and Hessians for efficient convergence.



---

## 4. Bundle Adjustment
Bundle adjustment is a comprehensive optimization technique for multi-view reconstruction. It minimizes the overall reprojection error across all views by refining both camera parameters and 3D point positions.

### Mathematical Formulation:
1. Solve for parameter updates using:

\[
\Delta p = (J^T J + \lambda I)^{-1} J^T \epsilon
\]

Where:
- \( J \): Jacobian matrix.
- \( \lambda \): Damping factor.
- \( \epsilon \): Error vector.

2. Exploit the block matrix structure to simplify computations for large datasets.

### Advantages:
- Efficient handling of large-scale systems.
- Accommodates missing data.
- Balances computational efficiency with numerical stability.

---

## Conclusion
These techniques form the foundation of modern 3D computer vision systems. From Tomasi-Kanade’s linear solutions to advanced numerical optimization like bundle adjustment, they enable accurate and scalable reconstructions by addressing ambiguity, noise, and computational challenges.
