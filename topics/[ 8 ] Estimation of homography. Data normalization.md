# Estimation of Homography

Homography estimation involves determining the $$3 \times 3$$ transformation matrix $$H$$ that relates two planes in projective space. This is done using point correspondences between two images of a planar scene.

## Steps for Homography Estimation:
1. **Collect Point Correspondences**:
   - Identify at least four pairs of corresponding points in the two images. More points improve robustness.
2. **Data Normalization**:

Elements in coefficient should be in the same order of magnitude

Translation: origo should be at the center of gravity

Scale: spread should be set to $$\sqrt{2}$$

   - Normalize the coordinates of the points to improve numerical stability. This involves:
     - Translating the centroid of points to the origin.
     - Scaling the points so that the average distance from the origin is $$\sqrt{2}$$.
4. **Construct Linear Equations**:
   - For each point correspondence $$(x, y) \leftrightarrow (x', y')$$, generate two equations using the homography relation:
     $$\[
     x' = \frac{h_{11}x + h_{12}y + h_{13}}{h_{31}x + h_{32}y + h_{33}},\,
     y' = \frac{h_{21}x + h_{22}y + h_{23}}{h_{31}x + h_{32}y + h_{33}}
     \]$$
   - Rewrite these in a linear form for all correspondences.
5. **Solve for $$H$$**:
   - Use methods like Singular Value Decomposition (SVD) to solve the linear system and estimate $$H$$.
6. **De-Normalization**:
   - Transform $$H$$ back to the original coordinate system using the inverse normalization transformations.

## Importance of Data Normalization:
- **Stability**: Ensures computations are numerically stable, especially for poorly scaled data.
- **Accuracy**: Prevents errors caused by differences in scale, skew, or coordinate magnitude.
- **Convergence**: Improves the performance of optimization algorithms like RANSAC.

Normalization is a key preprocessing step for reliable homography estimation, particularly in real-world, noisy datasets.
