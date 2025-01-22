# Stereo vision for planar motion.
Stereo vision for planar motion is a technique used to estimate depth and motion in environments where objects are primarily moving in a plane, such as ground vehicles or robotic systems operating on flat surfaces.

When we restrict the motion to a plane, we make a key simplification: instead of tracking objects moving freely in 3D space, we assume that the objects or the camera itself are moving within a flat, two-dimensional plane. This assumption significantly reduces the complexity of motion estimation, since we no longer need to estimate full 3D transformations, but rather we only need to consider motion along the plane and rotations around it.

The centeral idea is that the transformation between corresponding points across the two stere views can be described by a homography. A homography is a transformation that relates two views of the same plane in 3D space. This transformation encompasses translation, rotation, and scaling within the plane, but crucially it doesn't account for any motion that moves an object out of the plane.

Given the homography, we can estimate the motion of the camera or objects in the scene. This is possible because, for planar motion, the relationship between the image coordinates and the real-world coordinates can be simplified. Instead of computing full 3D transformations for each point, we only need to estimate the parameters of the homography matrix.

The homography matrix $𝐻$ relates the two image planes through the equation:

$$
s_2
\begin{bmatrix}
x_2 \\
y_2 \\
1
\end{bmatrix}
= H
\begin{bmatrix}
x_1 \\
y_1 \\
1
\end{bmatrix}
$$
