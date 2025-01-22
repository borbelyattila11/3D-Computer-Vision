# Calibration of perspective camera using a spatial calibration object: Estimation and decomposition of projection matrix.
To calibrate a perspective camera using a spatial calibration object, the goal is to estimate the camera's projection matrix $P$, which relates 3D world coordinates to 2D image coordinates. The projection matrix is typically a 3x4 matrix and consists of the intrinsic parameters and the extrinsic parameters.

#### Steps
1. **Setup Calibration Object:** Use a known 3D calibration object (checkboard pattern, planar grid, 3D object with known geometry)
2. **Capture Images:** Take multiple images of the calibration object from different angles and distances.
3. **Detect 2D Points:** In each captured image, detect the 2D projections of the known 3D points. These are the 2D image coordinates, denoted as $(x_i, y_i)$, corresponding to the 3D world coordinates $(X_i, Y_i, Z_i)$.
4. **Set up the Projection Equation:** The basic perspective projection formula can be written as:

$$
\begin{bmatrix}
  x_i \\
  y_i \\
  1
\end{bmatrix}
 =  P *
\begin{bmatrix}
  X_i \\
  Y_i \\
  Z_i \\
  1
\end{bmatrix} $$

5. **Estimation of the Projection Matrix:** Using the 2D-3D correspondence solve the projection matrix P. Each 2D point provides two equations (for $x_i$ and $y_i$) and the matrix equation can be solved using methods like Singular Value Decomposition.
6. **Decomposition of the Projection Matrix:** The projection matrix P can be decomposed into:

$P = K * [R | t]$

Where:
- $K$ is the intrinsic matrix, containing the focal lengths and principal point.
- $R$ is the rotation matrix, representing the camera's orientation in world space.
- $t$ is the translation vector, representing the camera's position in world space.

To extract K, R and t, perform the following steps:
- Decompose the matrix $P$ using QR decomposition to isolate the intrinsic matrix K.
- The matrix $R$ is derived by adjusting the scaled rotation portion, and $t$ can be determined from the translation part.

7. **Refinement with Non-Linear Optimization:** After the initial estimation, refine the parameters using non-linear optimization techniques, minimizing the reprojection error.
8. **Calibration Quality:** Evaluate the calibration quality by checking the reprojection error for all points.
