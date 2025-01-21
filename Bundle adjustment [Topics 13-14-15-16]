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
