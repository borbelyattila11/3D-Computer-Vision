# Estimation of Essential and Fundamental Matrices

## 1. Estimation of Fundamental and Essential Matrices

### Fundamental Matrix (F)
The **fundamental matrix** relates corresponding points between two images in uncalibrated stereo vision:

$$\[
x_2^T F x_1 = 0
\]$$

where $$x_1$$ and $$x_2$$ are corresponding points in homogeneous coordinates from the first and second image, respectively. The fundamental matrix encodes the epipolar constraint.

### Essential Matrix (E)
The **essential matrix** is used in calibrated stereo vision and relates normalized camera coordinates:

$$\[
x_2^T E x_1 = 0
\]$$

where $$x_1$$ and $$x_2$$ are in normalized camera coordinates. The essential matrix is computed as:

$$\[
E = K_2^T F K_1
\]$$

where $$K_1$$ and $$K_2$$ are the intrinsic camera matrices for the two views.

### Steps to Estimate Fundamental and Essential Matrices
1. **Feature Matching**: Detect keypoints and match points between the two images using algorithms like SIFT, SURF, or ORB.
2. **Compute the Fundamental Matrix**: Use the **eight-point algorithm** or **RANSAC-based robust methods**.
3. **Compute the Essential Matrix**: If camera intrinsics are known, compute:

$$\[
E = K_2^T F K_1
\]$$

---

## 2. Data Normalization

Normalization improves numerical stability.

### Steps for Normalization
1. Compute the centroid of points.
2. Scale the points so their mean distance from the origin is $$\sqrt{2}$$ for image points or $$\sqrt{3}$$ for 3D points.
3. Apply the normalization transformation matrix:

$$\
T = \begin{bmatrix}
s & 0 & -sx_c \\
0 & s & -sy_c \\
0 & 0 & 1
\end{bmatrix}
\$$

   where $$s$$ is the scaling factor and $$(x_c, y_c)$$ is the centroid.

Apply $$T$$ to all points before computing the fundamental or essential matrix.

---

## 3. Decomposition of Essential Matrix

To decompose the essential matrix $$E$$ into rotation $$R$$ and translation $$t$$:

1. Compute the singular value decomposition (SVD) of $$E$$:

$$\[
E = U \Sigma V^T
\]$$

   where $$\Sigma = \text{diag}(1, 1, 0)$$.

2. Use the matrices:

$$\
W = \begin{bmatrix} 0 & -1 & 0 \\
1 & 0 & 0 \\
0 & 0 & 1 \end{bmatrix}
\$$
   
   and
   
$$\
Z = \begin{bmatrix} 0 & 1 & 0 \\
-1 & 0 & 0 \\ 
0 & 0 & 0 \end{bmatrix}
\$$

3. Possible solutions for $$R$$ and $$t$$:

   $$\[
   R_1 = UWV^T, \quad R_2 = UW^TV^T, \quad t = U[:,2]
   \]$$

4. Choose the solution where points are in front of both cameras.

---

This process is fundamental in stereo vision applications like 3D reconstruction and camera pose estimation.
