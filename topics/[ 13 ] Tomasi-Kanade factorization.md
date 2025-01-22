### Tomasi-Kanade Factorization: Multi-View Reconstruction with Orthogonal and Weak-Perspective Projections

The **Tomasi-Kanade factorization method** is a foundational technique in 3D computer vision for **multi-view reconstruction** using simplified camera models, specifically **orthogonal and weak-perspective projections**. The key idea is to decompose a matrix of tracked 2D points from multiple frames into two matrices representing the motion and structure of the scene.

---

#### Key Concepts

1. **Measurement Matrix (W)**:  
   Contains stacked coordinates of tracked points across frames.
   
$$W = MS$$

   Here, $$M$$ represents camera motion parameters, and $$S$$ represents the 3D structure.

3. **Rank Constraint**:  
   The matrix $$W$$ has a maximum rank of 3 under noiseless conditions due to the nature of 3D point representations.

4. **Factorization using Singular Value Decomposition (SVD)**:  
   - The top three singular values are retained to reduce noise and compute the factorization:
     
$$
W = USV^T \rightarrow W' = U'S'V'^T
$$  
  - $$M_{\text{aff}}$$ and $$S_{\text{aff}}$$ are obtained for the affine approximation.

4. **Affine Ambiguity**:  
   Infinite factorizations exist since $$W = (MQ^{-1})(QS)$$. A matrix $$Q$$ is introduced to resolve this ambiguity, constrained by orthonormality conditions on the motion vectors.

5. **Metric Constraints and Ambiguity Removal**:  
   - Constraints ensure real camera geometry:


$$r_{i1}^T r_{i1} = 1, \quad r_{i1}^T r_{i2} = 0$$

   - Solving a linear system involving $$QQ^T = L$$ determines $$Q$$.

6. **Weak-Perspective Adaptation**:  
   Similar to orthogonal projection but without unit length constraints. This introduces proportional scaling rather than fixed scaling.

---

#### Summary of Factorization Steps

1. Center coordinates to the origin of gravity.
2. Compute SVD to obtain affine factors $$M_{\text{aff}}$$ and $$S_{\text{aff}}$$.
3. Apply metric constraints to compute matrix $$Q$$.
4. Use $$Q$$ to finalize metric reconstruction, yielding $$M$$ and $$S$$.

---

The Tomasi-Kanade factorization method is linear, making it computationally simpler than full perspective models. It is suitable for situations where perspective distortions are small or negligible.
