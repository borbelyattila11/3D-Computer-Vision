# Computer Vision: Camera Models and Calibration

This document comprehensively explains key concepts in computer vision, focusing on geometric camera models, camera calibration methods, and homography. It is structured to discuss models of cameras, calibration techniques, homography transformations, and associated error minimization processes.

---

## 1. Camera Models

### Perspective Camera
The **perspective (pin-hole) camera** model approximates a real camera by considering a focal point \( C \) and an image plane \( \phi \). Every point in the scene projects through \( C \) onto \( \phi \).  
**Projection equations:**
\[
u = \frac{f k_u}{Z_c} X_c + u_0, \quad v = \frac{f k_v}{Z_c} Y_c + v_0
\]
Here, \( f \) is the focal length, \( k_u \) and \( k_v \) are pixel size constants, and \( (u_0, v_0) \) is the principal point.

The intrinsic camera matrix \( K \) is:
\[
K = \begin{bmatrix}
f k_u & 0 & u_0 \\
0 & f k_v & v_0 \\
0 & 0 & 1
\end{bmatrix}
\]

### Orthogonal Projection
In **orthogonal projection**, depth variations are negligible, assuming parallel rays project the 3D scene onto the image plane:
\[
u = k X, \quad v = k Y
\]
where \( k \) is a scaling factor. Orthogonal projection models do not account for perspective distortion and are less complex.

### Weak-Perspective Camera
The **weak-perspective camera** assumes minimal depth variation across an object, simplifying projection:
\[
u = \frac{f k}{\tilde{Z}_c} X_c, \quad v = \frac{f k}{\tilde{Z}_c} Y_c
\]
where \( \tilde{Z}_c \) is the average depth. This model reduces complexity but sacrifices accuracy compared to full perspective projection.

---

## 2. Calibration of Perspective Camera Using a Spatial Object

Calibration aligns the camera’s image with 3D world coordinates by estimating the **projection matrix** \( P \):
\[
P = K R [I | -t]
\]
where \( K \) is the intrinsic matrix, \( R \) is the rotation, and \( t \) is the translation.

### Estimation of Projection Matrix
Given point correspondences \( X \rightarrow u \), the projection matrix is estimated using:
\[
A p = 0
\]
where \( p \) represents the flattened matrix \( P \). For over-determined systems, **Singular Value Decomposition (SVD)** minimizes:
\[
\|A p\| \quad \text{subject to} \quad \|p\| = 1
\]

### Decomposition
The matrix \( P \) is decomposed using RQ decomposition to separate rotation and intrinsic parameters:
\[
t = -R^T K^{-1} p_4
\]

---

## 3. Chessboard-Based Calibration of Perspective Cameras

Chessboard patterns offer a robust method for calibration using easily detected corner points.

### Intrinsic Parameter Computation
The homography between the chessboard plane and the image plane:
\[
H \sim K [r_1 \ r_2 \ t]
\]
yields the intrinsic matrix \( K \). Linear constraints on \( H \) provide:
\[
S = K^{-T} K^{-1}
\]
From multiple images, \( S \) is computed to extract focal lengths and principal point.

### Radial Distortion
Radial distortion bends straight lines into curves, modeled by:
\[
L(r) = 1 + \kappa_1 r^2 + \kappa_2 r^4
\]

### Tangential Distortion
Accounts for decentering effects:
\[
x' = x + [2 p_1 x y + p_2 (r^2 + 2 x^2)]
\]
\[
y' = y + [p_1 (r^2 + 2 y^2) + 2 p_2 x y]
\]

---

## 4. Plane-Plane Homography

Homography transforms points between two planes. For points \( X \) and \( X' \):
\[
X' \sim H X
\]
where \( H \) is a 3x3 transformation matrix. It is used for **rectifying road surfaces** and constructing **panoramic images** by stitching together views:
\[
H = K_2 R_2 R_1^T K_1^{-1}
\]

---

## 5. Estimation of Homography and Data Normalization

### Linear Estimation
Homography \( H \) is estimated using point correspondences \( u \rightarrow u' \):
\[
A h = 0
\]
with constraints on \( h \) to prevent trivial solutions. SVD provides a least-squares solution.

### Data Normalization
Coordinates are normalized by translating the centroid to the origin and scaling to a unit variance, enhancing numerical stability:
\[
T = \begin{bmatrix}
s & 0 & -s \mu_x \\
0 & s & -s \mu_y \\
0 & 0 & 1
\end{bmatrix}
\]
Normalized coordinates improve homography estimation accuracy.

---

This document provides a foundational understanding for practical applications like 3D reconstruction, object tracking, and augmented reality.
