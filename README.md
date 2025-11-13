# Habitat_Selection_Analysis
Using lidar-derived three-dimensional habitat structure variables, a habitat selection study of Francois's langur was conducted through random forest and optimal generalized liner models.
# The title of the paper is:
UAV-borne LiDAR reveals three-dimensional habitat selection patterns of François' langurs in complex karst landscapes
# Code Explanation:
The code for this study is mainly divided into four parts:

1. Variable Extraction: Extracting 3D structural variables of habitats from point cloud data derived from LiDAR. Since our ground point classification is performed in DJI Terra software, the classification process is not shown in this code; the point cloud data used has already been classified.

2. 10-Fold Cross-Validation: This code mainly involves performance validation of Random Forest and Generalized Linear Model (GLM). The original dataset is divided into 10 parts. In each validation, one part is used as the validation set, and the rest are used as the training set, thus running the model ten times. This part of the code is mainly divided into two parts: one is the 10-fold cross-validation for the RF model, and the other is the 10-fold cross-validation for the GLM model. The model used for validation in the GLM model is the top-level model (deletaAIC=0) after training each fold on the training set.

3. SHAP Analysis: We used the entire dataset for training RF and GLM. We selected all candidate GLM models with ΔAICc < 2 using AICc, obtained the AICc weights for each model, and then calculated the SHAP value for each candidate model. We multiplied the SHAP matrix of each model by its corresponding AICc weight, and then summed all the weighted SHAP matrices to obtain the final SHAP value considering model uncertainty. We used kernelshap to interpret the trained RF model, using the entire dataset as the explanatory set and the background set. We calculated the marginal contribution of each feature to the predicted probability for each sample. Unlike GLM, RF does not require model averaging because Random Forest is already an ensemble model.

4. Response Curve and Partial Dependency Plotting: For important variables included in the optimal GLM, we predicted probabilities by fixing other variables at their mean and changing the target variable alone. RF calculated the marginal effect using a partial dependence plot and normalized it to the 0-1 interval.
