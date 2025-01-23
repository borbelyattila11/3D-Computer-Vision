# Camera Models

## Perspective Camera (pinhole camera)
Perspective camera is a model used to simulate the way a real-world camera captures images from a 3D scene onto a 2D plane. The perspective camera assumes that light rays emanate from a 3D scene, pass through a point known as the camera center, and project onto a 2D image plane. The model creates realistic depiction of objects, where their apparent size decreases with distance, mimicking human vision. Due to the light intersecting at a single point (the pinhole) the resulting image on the image plane is inverted.

A 3D point (X, Y, Z) in the world coordinate system is projected onto a 2D image point (x, y) using the following equations:

$x = \frac{fX}{Z},$ $y = \frac{fY}{Z}$ where $f$ is the focal length, and $Z$ is the depth of the point from the camera.

#### Fundamental Parameters:
- **center of projection** is the point where the pinhole aperture is located
- **focal length** is the distance between the center of the projection and the image plane
- **optical axis** is the line perpendicular to the image plane and passing through the center of projection
- **principal point** is defined as the point of intersection between the optical axis and the image plane

## Orthogonal Projection (Orthographic Camera)
Orthographic projection is a means of representing three-dimensional objects in two dimensions. In orthogonal projection, objects maintain their size regardless of distance from the camera. There is no perspective distortion, and objects that are farther away from the camera appear the same size as objects that are closer.

- An orthographic camera is often described with fewer intrinsic parameters since it does not include focal length or distortion.

## Weak-Perspective Camera
A "weak" perspective projection uses the same principles of an orthographic projection, but requires the scaling factor to be specified, thus ensuring that closer objects appear bigger in the projection, and vice versa. The weak-perspective model thus approximates perspective projection while using a simpler model, similar to the pure (unscaled) orthographic perspective. It is a reasonable approximation when the depth of the object along the line of sight is small compared to the distance from the camera, and the field of view is small.

#### Summary
- **Perspective Camera:** Exhibits realistic perspective distortions (objects appear smaller with increasing distance).
- **Orthogonal Projection:** No perspective distortion, making it useful for technical drawings, maps, and other applications requiring scale invariance.
- **Weak-Perspective Camera:** A simplified perspective model, useful when depth differences are minimal but some perspective effects are still needed.
