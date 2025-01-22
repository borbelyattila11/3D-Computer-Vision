# Calibration of perspective camera using a spatial calibration object: Estimation and decomposition of projection matrix.
To calibrate a perspective camera using a spatial calibration object, the goal is to estimate the camera's projection matrix $P$, which relates 3D world coordinates to 2D image coordinates. The projection matrix is typically a 3x4 matrix and consists of the intrinsic parameters and the extrinsic parameters.

#### Steps
1. **Setup Calibration Object:** Use a known 3D calibration object (checkboard pattern, planar grid, 3D object with known geometry)
