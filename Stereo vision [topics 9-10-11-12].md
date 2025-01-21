# Epipolar Geometry and Stereo Vision: Comprehensive Overview

## 1. Basics of Epipolar Geometry
Epipolar geometry is fundamental in stereo vision, describing the geometric relationship between two camera views of a 3D scene. The key concepts are:
- **Epipolar Plane**: A plane defined by a 3D point and the optical centers of two cameras.
- **Epipoles**: Points where the baseline connecting the two cameras intersects the image planes.
- **Epipolar Lines**: The intersection of the epipolar plane with each image plane. Corresponding points between images lie on these lines.

The **epipolar constraint** reduces point matching to a one-dimensional search along epipolar lines rather than a two-dimensional search. This relationship is captured by two matrices:
- **Essential Matrix (E)**: Used with calibrated cameras. It encodes rotation \( R \) and translation \( t \), with properties ensuring rank 2 and two equal non-zero singular values.
- **Fundamental Matrix (F)**: Generalizes epipolar geometry to uncalibrated cameras. It relates pixel coordinates directly and is computed as \( F = K_2^{-T} E K_1^{-1} \), where \( K_1 \) and \( K_2 \) are camera calibration matrices.

**Rectification** transforms images so that epipolar lines become horizontal, simplifying matching to a scanline search. Rectified images enable efficient 1D correspondence matching.

---

## 2. Estimation of Essential and Fundamental Matrices
Accurate estimation of these matrices is crucial for 3D reconstruction:
- **Eight-Point Algorithm**: Requires at least eight point correspondences. This method normalizes data by translating points to the centroid and scaling them to an average distance of \( \sqrt{2} \).
- **Singular Value Decomposition (SVD)**: Used to enforce the rank-2 constraint on the essential matrix. The decomposition \( E = U \Sigma V^T \) provides rotation and translation up to scale, producing four possible solutions. The correct one places the reconstructed points in front of both cameras.

Normalization improves numerical stability, ensuring that matrix entries remain well-scaled. Denormalization reverses this transformation after estimation.

---

## 3. Triangulation
Triangulation determines the 3D position of a point from its 2D correspondences in stereo images:
- **Standard Stereo**: Uses two parallel, calibrated cameras. Key parameters are the baseline \( b \), focal length \( f \), and disparity \( d \) (the horizontal difference between corresponding points). Depth \( Z \) is computed as \( Z = \frac{bf}{d} \).
- **Linear Triangulation**: Projects image points back into 3D space, forming rays that intersect (ideally) at the true point. In practice, noise causes a small gap, so the point halfway along the shortest line between the rays is taken.
- **Reprojection Error Minimization**: Refines triangulation results by adjusting 3D points and camera parameters to minimize the distance between projected and observed points.

Metric reconstruction from the essential matrix uses known intrinsic camera parameters. Projective reconstruction, suitable for uncalibrated cameras, is defined only up to a projective transformation.

---

## 4. Stereo Vision for Planar Motion
Planar motion models are common in autonomous vehicles, where movement is constrained to a plane:
- The translation vector \( t = [\rho \cos \alpha, 0, \rho \sin \alpha]^T \) lies in the XZ plane, with direction \( \alpha \).
- The rotation matrix \( R \) represents rotation around the Y-axis by angle \( \beta \).

The essential matrix for planar motion has a simplified structure with four non-zero elements:
\[ E = [t] \times R \propto \begin{bmatrix} 0 & -\sin \alpha & 0 \\ \sin(\alpha + \beta) & 0 & -\cos(\alpha + \beta) \\ 0 & \cos \alpha & 0 \end{bmatrix} \]

With semi-calibrated cameras, the fundamental matrix is similarly compact. Only two point correspondences are necessary for estimation, making this a computationally efficient special case. Robust estimation methods like RANSAC handle outliers effectively, ensuring accurate results even in real-world scenarios.

