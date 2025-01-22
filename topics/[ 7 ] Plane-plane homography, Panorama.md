# Plane-to-Plane Homography

A **homography** is a projective transformation that relates two views of the same planar surface. In the context of computer vision and image processing, a homography is represented as a $$3 \times 3$$ matrix $$H$$ and relates the points $$(x, y)$$ on one plane to points $$(x', y')$$ on another plane through the equation:

$$
\begin{bmatrix}
  x' \\
  y' \\
  1
\end{bmatrix}
 =  H
\begin{bmatrix}
  x \\
  y \\
  1
\end{bmatrix} $$

where $$H$$ is a $$3 \times 3$$ matrix defined up to a scale factor. It can be estimated if you have at least four pairs of corresponding points between the two planes.
-Homography estimation requires solving a system of linear equations for the unknown homography matrix 𝐻
-If there are more than four point correspondences, the system becomes overdetermined, meaning there are more equations than unknowns.
SVD is ideal for finding the best least-squares solution in such cases.

## Steps to Compute Plane-to-Plane Homography
1. **Collect Point Correspondences**: Identify at least four points on the plane in one image and their corresponding locations in the other image.
2. **Construct a Linear System**: Use the point correspondences to set up a system of equations derived from the homography formula.
3. **Solve for $$H$$**: Use methods like Singular Value Decomposition (SVD) to solve the system and estimate $$H$$.
4. **Apply Transformation**: Use the computed $$H$$ matrix to map points or images from one plane to the other.

# Panoramic Images Using Homographies

A **panorama** is created by stitching multiple overlapping images together. When the images are taken from the same camera position (pure rotation about the optical center), they can be related through homographies.

## Steps to Create Panoramas with Homographies
1. **Image Acquisition**: Capture a series of overlapping images with a consistent rotation.
2. **Feature Detection and Matching**: Identify keypoints in the overlapping regions (e.g., using SIFT, ORB, or SURF) and find correspondences.
3. **Estimate Homography**:
   - Use RANSAC to robustly estimate the homography $$H$$ between pairs of images.
4. **Warp Images**:
   - Transform images to a common coordinate frame using the homography matrices.
   - Use backward mapping to ensure proper interpolation.
5. **Blend Images**:
   - Seamlessly blend overlapping regions to reduce artifacts. Techniques include feathering, multi-band blending, or using Laplacian pyramids.
6. **Generate the Panorama**:
   - Align all images in a unified coordinate frame and crop or fill missing regions.

## Applications of Homography in Panoramas
- Virtual tours and 360-degree imagery.
- Image mosaicking.
- Video stabilization when the scene can be approximated as planar.

---
