# Computer Vision: Camera Models and Calibration

This document explains key concepts in camera models, calibration techniques, and homography in computer vision. It covers perspective and weak-perspective cameras, calibration of projection matrices, homography transformations, and error minimization methods.

---

## 1. Camera Models

### Perspective Camera
The **perspective (pin-hole) camera** model is a geometric approximation of real cameras. It assumes a focal point \( C \) and an image plane \( \phi \). Each point in 3D projects through \( C \) to ($\phi$).

**Projection equations**:
$u = \frac{f k_u}{Z_c} X_c + u_0, \quad v = \frac{f k_v}{Z_c} Y_c + v_0$
where:
- \( f \) is the focal length,
- \( k_u \) and \( k_v \) are pixel scaling factors,
- \( (u_0, v_0) \) is the principal point.

The intrinsic camera matrix \( K \) is:
\[
K = \begin{bmatrix}
f k_u & 0 & u_0 \\
0 & f k_v & v_0 \\
0 & 0 & 1
\end{bmatrix}
\]

### Orthogonal Projection
In **orthogonal projection**, parallel rays are assumed:
\[
u = k X, \quad v = k Y
\]
This model is simpler but does not handle perspective distortion.

### Weak-Perspective Camera
The **weak-perspective camera** assumes negligible depth variation across objects:
\[
u = \frac{f k}{\tilde{Z}_c} X_c, \quad v = \frac{f k}{\tilde{Z}_c} Y_c
\]
where \( \tilde{Z}_c \) is the average object depth.

---

## 2. Calibration of Perspective Camera Using a Spatial Object

Calibration uses known 3D points to estimate the **projection matrix**:
\[
P = K R [I | -t]
\]
where:
- \( K \) is the intrinsic matrix,
- \( R \) is the rotation matrix,
- \( t \) is the translation vector.

### Projection Matrix Estimation
Given correspondences \( X \rightarrow u \), the projection matrix \( P \) is estimated from:
\[
A p = 0
\]
where \( A \) contains point data, and \( p \) represents elements of \( P \). **Singular Value Decomposition (SVD)** minimizes:
\[
\|A p\| \quad \text{subject to} \quad \|p\| = 1
\]

### Decomposition
Decomposing \( P = KR[I | -t] \):
\[
t = -R^T K^{-1} p_4
\]

---

## 3. Chessboard-Based Calibration of Perspective Cameras

Chessboard calibration uses detected corners for intrinsic parameter estimation.

**Homography** between the chessboard and image plane:
\[
H \sim K [r_1 \ r_2 \ t]
\]
where \( r_1 \) and \( r_2 \) are rotation vectors.

### Radial Distortion
Radial distortion bends straight lines, corrected using:
\[
L(r) = 1 + \kappa_1 r^2 + \kappa_2 r^4
\]

### Tangential Distortion
This accounts for decentering:
\[
x' = x + [2 p_1 x y + p_2 (r^2 + 2 x^2)]
\]
\[
y' = y + [p_1 (r^2 + 2 y^2) + 2 p_2 x y]
\]

---

## 4. Plane-Plane Homography

A homography transforms points between planes:
\[
X' \sim H X
\]
It rectifies planar surfaces or constructs panoramic images:
\[
H = K_2 R_2 R_1^T K_1^{-1}
\]

---

## 5. Estimation of Homography and Data Normalization

### Linear Estimation
Using correspondences \( u \rightarrow u' \), homography \( H \) solves:
\[
A h = 0
\]

### Data Normalization
Normalization centers and scales points:
\[
T = \begin{bmatrix}
s & 0 & -s \mu_x \\
0 & s & -s \mu_y \\
0 & 0 & 1
\end{bmatrix}
\]

Normalization improves stability for homography estimation.
