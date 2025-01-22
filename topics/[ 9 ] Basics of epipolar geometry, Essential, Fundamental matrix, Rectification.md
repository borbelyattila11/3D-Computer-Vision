### Basics of Epipolar Geometry

Epipolar geometry is a fundamental concept in computer vision and 3D reconstruction, describing the geometric relationship between two views of a 3D scene captured by two cameras.

#### Key Elements:
1. **Epipolar Plane**:
   - The plane formed by a 3D point and the optical centers of two cameras.

2. **Epipolar Line**:
   - The intersection of the epipolar plane with the image planes of the two cameras.
   - For a point in one image, its corresponding point in the second image lies on the corresponding epipolar line.

3. **Epipoles**:
   - The points where the line connecting the two camera centers (the baseline) intersects the image planes.
   - In stereo setups, the epipole is the projection of one camera center onto the other camera’s image plane.

#### Key Property:
The correspondence of points between two images is constrained to lie on their respective epipolar lines, reducing the search from 2D to 1D.

---

### Essential and Fundamental Matrices

Both matrices encode the epipolar geometry but differ in their requirements and use cases:

#### Fundamental Matrix (F):
- A $$3 \times 3$$ matrix that maps a point in one image to its corresponding epipolar line in the other image.
- Works in pixel coordinates and is independent of the intrinsic parameters of the cameras.
- Relationship:
  $$\[
  x_2^T F x_1 = 0
  \]$$
  Where $$x_1$$ and $$x_2$$ are homogeneous image coordinates in the first and second images, respectively.

#### Essential Matrix (E):
- A $$3 \times 3$$ matrix that also encodes epipolar geometry but is specific to calibrated cameras.
- Requires intrinsic camera parameters.
- Relates the normalized coordinates of points:
  $$\[
  \hat{x}_2^T E \hat{x}_1 = 0
  \]$$
  Where $$\hat{x}_1$$ and $$\hat{x}_2$$ are normalized image coordinates (i.e., coordinates in the camera coordinate system).

#### Relationship Between F and E:
$$\[
F = K_2^{-T} E K_1^{-1}
\]$$
Where $$K_1$$ and $$K_2$$ are the intrinsic calibration matrices of the two cameras.

---

### Rectification

#### Purpose:
To simplify stereo matching by transforming the image planes so that epipolar lines become horizontal and aligned between the two images.

#### Process:
1. **Rotation and Translation**:
   - Adjust the cameras’ orientations virtually to make their image planes coplanar.
2. **Homography**:
   - Apply a transformation (homography) to align epipolar lines horizontally.
3. **Output**:
   - Two rectified images where corresponding points lie on the same row, enabling efficient stereo correspondence search.

#### Applications:
- Stereo vision and disparity computation.
- 3D reconstruction and depth estimation.

---

### Summary Workflow:
1. Use the **fundamental matrix** to establish epipolar constraints for uncalibrated images.
2. Use the **essential matrix** for calibrated systems to enforce the same constraints in normalized space.
3. Apply **rectification** to simplify and accelerate stereo correspondence tasks.
