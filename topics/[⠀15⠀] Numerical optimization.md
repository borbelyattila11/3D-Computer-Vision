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
