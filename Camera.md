# Computer Vision: Camera Models and Calibration

This lecture provides a comprehensive overview of geometric camera models, homography, and camera calibration, essential for understanding the principles of computer vision.

---

## 1. Camera Models

### Perspective (Pin-Hole) Camera
The perspective camera model, equivalent to the pin-hole camera, provides a geometric approximation of real optics. It assumes a focal point \( C \) and an image plane \( \phi \), connected by optical rays from 3D scene points.

#### Notations and Transformations
- World coordinates: \( X = [X, Y, Z]^T \)
- Camera coordinates: \( X_c = [X_c, Y_c, Z_c]^T \)
- Image coordinates: \( u = [u, v]^T \)

Transformations between world and camera coordinates include:
\[
X_c = R(X - t)
\]
\[
X_c = R[I| -t] \begin{bmatrix} X \\ 1 \end{bmatrix}
\]

Projection to image coordinates:
\[
u = \frac{f k_u}{Z_c} X_c + u_0
\]
\[
v = \frac{f k_v}{Z_c} Y_c + v_0
\]

The intrinsic calibration matrix \( K \) is:
\[
K = \begin{bmatrix}
f k_u & 0 & u_0 \\
0 & f k_v & v_0 \\
0 & 0 & 1
\end{bmatrix}
\]

### Weak-Perspective Camera
Assumes the object depth variation is negligible compared to the camera distance. Projection simplifies to scaled orthographic projection:
\[
u = \frac{f k}{\tilde{Z}_c} X_c + u_0
\]
\[
v = \frac{f k}{\tilde{Z}_c} Y_c + v_0
\]

Weak-perspective models eliminate scale ambiguity but may sacrifice accuracy.

### Model Comparison
- **Perspective Projection**: Accurate, with size changes and perspective distortion.
- **Weak-Perspective Projection**: Approximates real projection; simpler with fewer parameters.

### Back-Projection
For a 2D image point, the corresponding 3D point is ambiguous due to depth. Back-projection produces a line in 3D space.

---

## 2. Homography

### Definition
A homography is a projective transformation between two planes. It maps point correspondences as:
\[
u' \sim H u
\]
where \( H \) is a non-singular matrix.

### Estimation
Linear estimation involves solving:
\[
A h = 0
\]
where \( A \) depends on point correspondences and \( h \) represents homography parameters.

For robust estimation, techniques like RANSAC handle outliers.

### Geometric Error Minimization
Non-linear refinement minimizes:
\[
\sum_i d(u_i', H u_i)^2 + d(u_i, H^{-1} u_i')^2
\]

---

## 3. Camera Calibration

### Objectives
Calibration estimates intrinsic parameters (focal length, principal point) and extrinsic parameters (position, orientation).

#### Calibration Methods
1. **Spatial Object Calibration**: Uses a known 3D object (e.g., calibration cube).
2. **Chessboard Calibration**: Common due to ease of use and software support (e.g., OpenCV).

#### Linear Estimation
Projection matrix \( P \) is estimated using correspondences:
\[
u \sim P X
\]
Solving \( Ap = 0 \) yields \( P \), decomposed as \( P = K R [I| -t] \).

#### Chessboard-Based Calibration
Homography estimation between the chessboard plane and image provides:
\[
H \sim K [r_1 \ r_2 \ t]
\]
where \( r_1, r_2 \) are rotation vectors.

### Radial Distortion
Radial distortion (barrel or pincushion) affects projection accuracy. It is corrected using:
\[
u = u_c + L(r) (u - u_c)
\]
with \( L(r) = 1 + \kappa_1 r^2 + \kappa_2 r^4 \).

---

## Summary
This lecture covers essential concepts for geometric modeling, homography, and calibration, forming a foundation for advanced computer vision tasks.
