# Sequential RANSAC
Sequential RANSAC is a variation of the traditional RANSAC algorithm designed to identify and fit multiple models within a dataset. It operates sequentially, extracting one modle at a time, removing its inliers and then contiuing the process with the remaining data.

#### Steps
1. **Initialize:** Start with the full dataset.
2. **Fit a model using RANSAC:** Apply the standard RANSAC algorithm to find the best model that fits the data.
3. **Remove inliers:** Remove th einliers of the current model from the dataset. This step ensures that subsequent iterations do not consider points already explained by the previous model.
4. **Repeat:** Continue fitting models to the remaining data until the remaining points is too small or no significant inliers are found for a new model.

Sequential RANSAC can identify multiple distinct patterns in the data, due the multi model behavior.

# MultiRANSAC
MultiRANSAC is an extension of the standard RANSAC algorithm that aims to fit multiple models simultaneously rather than sequentially. This approach is particularly useful when the dataset contains multiple structures or patterns that overlap or coexist, and you want to identify all of them in a single process.

#### Steps
1. **Initialize:** tart by randomly selecting subsets of data for each model.
2. **Assign Points to Models:** For each point in the dataset, calculate its distance to all the current models. If a point doesn't fit any model, it is treated as an outlier.
3. **Refit Models:** Using the inliers assigned to each model, refine the model parameters.
4. **Repeat:** Repeat the process of reassigning points to models and refining the models until convergence or a maximum number of iterations is reached.
