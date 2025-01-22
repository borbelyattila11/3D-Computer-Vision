# Robust Fitting Methods (RANSAC)
RANSAC is an iterative algorithm used for robust parameter estimation in the precense of outliers. Particulary used where a significant portion of the data may be noisy or invalid.

#### Steps
1. **Construct the Trial Model:** Randomly pick a small subset of data points and build a trial model using these points.
2. **Identify inliers and outliers:** Use the trial model to check all the other data points. Points that are close to the model within a threshold are inliers, outside of the threshold are the outliers.
3. **Repeat the process:** Repeat the process for multiple times with different random subsets.
4. **Keep the best model:** Once all the iterations are ended find the best model.
