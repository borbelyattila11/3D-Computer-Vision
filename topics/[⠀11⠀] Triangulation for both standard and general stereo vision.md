# Triangulation for both standard and general stereo vision.
Triangulation in stereo vision refers to the process of determining the 3D position of a point by combining corresponding 2D observations from two or more camera views.

## Standard Stereo Vision
1. **Camera Calibration**
Calibrate the cameras to obtain intrinsic parameters (K) and extrinsic parameters (R, T)

2. **Correspondence Search**
Match point between the left and right images using feature detection and matching algorithms (SIFT, ORB). After matching, find the pixel coordinates ($u_L$, $v_L$) in the left image and ($u_R$, $v_R$) in the right image.

3. **Compute Disparity**
Disparity $d$ is calculated for each matched point:
$d = u_L - U_R$

4. **3D Reconstruction**
Reconstruct the 3D coordinates of the point P(X, Y, Z) in the camera coordinate system:
$Z = \frac{f * B}{d}$
$X = \frac{Z * (u_L - c_x)}{f}$
$Y = \frac{Z * (v_L - c_y)}{f}$

Where:
- **Z** is the depth (distance from the camera plane to the point)
- **X, Y** is the coordinates relative to the camera's optical center

## General Stereo Vision
For general stereo setups, cameras are not rectified, and their relative orientation (rotation 𝑅 and translation 𝑇) must be considered.
