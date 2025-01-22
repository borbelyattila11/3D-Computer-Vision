# Robust Fitting Methods (RANSAC)
RANSAC is an iterative algorithm used for robust parameter estimation in the precense of outliers. It is particularly effective in scenarios where a significant portion of the data may be noisy, incomplete, or corrupted, such as in computer vision, robotics, and 3D reconstruction.

#### Key Characteristics
- **Outlier Tolerance:** RANSAC is designed to handle data with outliers effectively by focusing on subsets of data points that are more likely to represent the true underlying model.
- **Iterative Approach:** Iteratively refining the model based on random subsets of data, ensuring that the model is robust against outliers.
- **Model Selection:** The best model is selected based on its ability to fit the majority of the data points.

#### Steps
1. **Construct the Trial Model:** Randomly pick a small subset of data points and build a trial model using these points.
2. **Identify inliers and outliers:** Use the trial model to check all the other data points. Points that are close to the model within a threshold are inliers, outside of the threshold are the outliers.
3. **Repeat the process:** Repeat the process for multiple times with different random subsets.
4. **Keep the best model:** Once all the iterations are ended find the best model.
