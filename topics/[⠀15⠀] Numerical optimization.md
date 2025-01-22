# Numerical optimization
In 3D computer vision, numerical optimization plays a crucial role in solving various problems, such as reconstructing 3D models, estimating camera parameters, and aligning point clouds.

#### 1. Gradient Method (Gradient Descent)
The gradient method is an iterative optimization technique that minimizes (or maximizes) a function by moving in the direction of the steepest descent (negative gradient).

$x_{k+1} = x_k - η∇f(x_k)$

Where:
- $η$ is the learning rate
- $∇f(x_k)$ is the gradient of the objective function at $x_k$

#### 2. Newton Method
Newton's method is a second-order optimization technique that uses the Hessian matrix (second derivatives) to achieve faster convergence, especially near the optimum.

$x_{k+1} = x_k - H^{-1}∇f(x_k)$

Where:
- $H$ is the Hessian matrix of second order derivatives of $f$

#### 3. Gauss-Newton Method
The Gauss-Newton method is a specialized variant of Newton's method for solving non-linear least squares problems. It approximates the Hessian matrix, avoiding its direct computation.

For a least squares problem:

$f(x) = \frac{1}{2} \sum{[r_i(x)]^2}$

**Steps:**
1. Compute the Jacobian matrix **$J$** where $J_{ij} = \frac{∂r_i}{∂x_j}$
2. Update:

$x_{k+1} = x_k - (J^TJ)^{-1}J^Tr$

#### 4. Levenberg-Marquardt Algorithm
The Levenberg-Marquardt algorithm (LMA) combines the Gauss-Newton method with gradient descent to improve convergence in non-linear least squares problems.

$x_{k+1} = x_k - (J^TJ + λI)^{-1}J^Tr$

Where:
- $λ$ is a damping factor
- $I$ is the identity matrix

If the update decreases the error, reduce $λ$ (move towards Gauss-Newton), but if the error increases, increase $λ$ (move towards gradient descent)

#### 5. Approximation by a Taylor Series
The Taylor series approximates a function $𝑓(𝑥)$ around a point $𝑥0$ using its derivatives. It's fundamental in deriving methods like Newton's and Gauss-Newton.

$f(x) ≈ f(x_0) + ∇f(x_0)^T(x - x_0) + \frac{1}{2}(x - x_0)^TH(x - x_0)$

Where:
- $∇f(x_0)$ is the gradient
- $H$ is the Hessian matrix
