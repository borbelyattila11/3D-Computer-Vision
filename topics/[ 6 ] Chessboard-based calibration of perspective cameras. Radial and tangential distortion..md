# Chessboard-based calibration of perspective cameras.
Used to determine the intrinsic and extrinsic parameters of perspective cameras.

#### Step 1: Capturing Images
Multiple images of a standard chessboard pattern are captured from different orientations and distances.

#### Step 2: Detecting the Corners
The corners of the chessboard squares are detected in the images.

#### Step 3: Mapping 2D Image Points to 3D World Points
The 3D positions of the chessboard corners (in the real world) are mapped to their corresponding 2D projections in the captured images.

#### Step 4: Optimization
The camera's intrinsic and extrinsic parameters are estimated using optimization techniques.

The intrinsic parameters include:
- Focal length ($f_x$, $f_y$)
- Principal point ($c_x$, $c_y$)
- Distortion coefficients

The extrinsic parameters include:
- Rotation and translation vectors for the chessboard relative to the camera.

# Lens Distortion
Lens distortion causes straight lines to appear curved and affects the accuracy of the calibration.

#### Radial Distortion
Radial distortion is caused by the spherical shape of the lens. It can result in a **Barrel distortion** (toward the edges) or **Pincushion distortion** (toward the center).

$x_{distorted} = x(1 + k_1r^2 + k_2r^4 + k_3r^6)$
$y_{distorted} = y(1 + k_1r^2 + k_2r^4 + k_3r^6)$

Where:
- $r = \sqrt{x^2 + y^2}$ is the radial distance from the principal point
- $k_1, k_2, k_3$ are the radial distortion coefficients

#### Tangential Distortion
Tangential distortion occurs due to the lens not being perfectly aligned with the imaging plane. It skews the image slightly in a tangential direction.

$x_distorted = x + [2p_1xy + p_2(r^2 + 2x^2)]$
$y_distorted = y + [p_1(r^2 + 2y^2) + 2p_2xy]$

Where:
- $p_1, p_2$ are the tangential distortion coefficients

## Calibration Output
After calibration, you obtain:
- **Camera matrix (K):**

$$
K = \begin{bmatrix}
f_x & 0 & c_x \\
0 & f_y & c_y \\
0 & 0 & 1
\end{bmatrix}
$$

- **Distortion coefficients:** $[k_1, k_2, p_1, p_2, k_3]$
- **Rotation and translation vectors** for each image
