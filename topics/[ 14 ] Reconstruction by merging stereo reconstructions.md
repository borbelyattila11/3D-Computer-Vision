### Reconstruction by Merging Stereo Reconstructions: Registration of Two Point Sets by a Similarity Transformation

Merging multiple stereo reconstructions into a unified 3D structure requires **registration of two point sets** using a **similarity transformation**. This approach aligns point clouds generated from different stereo image pairs by estimating the transformation parameters that best map one point set onto another.

---

#### Key Concepts

1. **Point Clouds and Coordinate Systems**:  
   - For stereo reconstruction, the coordinate system is typically fixed to the first camera.  
   - Two point clouds, $$\{p_i\}$$ and $$\{q_i\}$$, represent the 3D points from two different stereo views, where $$i = 1 \dots N$$ for $$N$$ common points.

2. **Similarity Transformation**:  
   The relationship between corresponding points in the two point clouds is expressed as:

$$q_i = s R p_i + t$$

   where:  
   - $$s$$ is the scale factor,  
   - $$R$$ is the rotation matrix,  
   - $$t$$ is the translation vector.

4. **Objective Function for Registration**:  
   To find the optimal transformation, the following cost function is minimized:

 $$\sum_{i=1}^{N} \| q_i - s R p_i - t \|^2$$

6. **Optimal Transformation Parameters**:  
   - **Translation (t)**:  
     The difference between the centers of gravity of the two point sets.
   - **Rotation (R)**:  
     Derived from the singular value decomposition (SVD) of matrix $$H$$, where:

$$H = \sum_{i=1}^{N} q_i' p_i'^T$$

     The optimal rotation is given by:

$$R = V U^T \quad \text{where} \quad H = USV^T$$

   - **Scale (s)**:
 
$$s = \frac{\sum_{i=1}^{N} q_i'^T R p_i'}{\sum_{i=1}^{N} p_i'^T p_i'}$$

---

#### Summary of Process

1. Extract corresponding points from both stereo reconstructions.
2. Compute the centers of gravity for both point clouds.
3. Use SVD to determine the rotation matrix $$R$$.
4. Calculate the optimal scale $$s$$.
5. Compute the translation vector $$t$$.
6. Apply the similarity transformation to merge the point clouds.

---

This method ensures an accurate and efficient merging of stereo reconstructions by aligning 3D structures through optimal similarity transformations, minimizing reconstruction errors.
