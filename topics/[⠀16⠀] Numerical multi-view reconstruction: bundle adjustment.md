### Summary on Bundle Adjustment from Multi-View Reconstruction

**Bundle Adjustment Overview**  
Bundle adjustment (BA) is a key optimization technique in numerical multi-view reconstruction. It refines the 3D structure and viewing parameters simultaneously to achieve the best fit between observed and predicted image features. It is commonly used after initial 3D reconstruction to improve accuracy.

**Core Concept**  
The objective is to minimize the reprojection error, defined as the difference between the observed image points and the projections of estimated 3D points onto the image planes. The parameters involved are:
- Camera parameters (intrinsic and extrinsic)
- 3D point coordinates

**Mathematical Formulation**  
The projected coordinates of the $$j$$-th point in the $$i$$-th frame depend on the camera parameters and the spatial coordinates of the point. The optimization is done using the **Levenberg-Marquardt (LM) algorithm**, which balances between gradient descent and Gauss-Newton methods for stable convergence.

- The LM update rule is:

$$\Delta p = \left( J^T J + \lambda I \right)^{-1} J^T \epsilon$$

where $$J$$ is the Jacobian matrix of partial derivatives, $$\lambda$$ is a damping factor, and $$\epsilon$$ is the error vector.

**Challenges and Solutions**  
1. **Large-Scale Optimization**  
   For large problems (e.g., 20 cameras and 1000 points), estimating thousands of parameters makes direct inversion computationally intensive. Therefore, **sparse** versions of the LM algorithm are employed, leveraging the sparsity of the Jacobian matrix.
   
2. **Normal Equations**
   The normal equation for solving bundle adjustment is block-structured:

$$\begin{bmatrix} U & X \\ 
X^T & V 
\end{bmatrix}
\begin{bmatrix}
\Delta m \\
\Delta s
\end{bmatrix} $$

$$ = $$ $$
\begin{bmatrix} 
\epsilon_m \\ 
\epsilon_s 
\end{bmatrix}$$


Efficient solutions involve inverting smaller submatrices instead of the entire matrix.

**Applications**  
Bundle adjustment is critical in applications like:
- Structure from motion (SfM)
- Simultaneous localization and mapping (SLAM)
- 3D modeling from images

In practice, it significantly improves geometric consistency across views by iteratively refining the solution until minimal reprojection error is achieved.


[Source](https://www.youtube.com/watch?v=lmj2Jk5tl60)
