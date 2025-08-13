📊 Bankruptcy Prediction – Model Development Pipeline
1. Choosing the Initial Models
Models: Logistic Regression, Random Forest, XGBoost.

Rationale:

Logistic Regression → interpretable baseline.

Random Forest → handles non-linear interactions & robust to noise.

XGBoost → high predictive power with noisy data.

Avoid unsupervised clustering; leverage labels for probability estimation.

2. Data Pre-processing
Scale for Logistic Regression; minimal scaling for tree models.

One-Hot Encode categorical variables.

Use Pipelines to avoid train/test transformation mismatch.

3. Handling Class Imbalance
SMOTE for oversampling rare bankruptcy cases.

class_weight for Logistic Regression to reduce computation.

Stratified CV to maintain class ratios.

Apply SMOTE only on training data to prevent leakage.

4. Outlier Detection & Treatment
Retain informative outliers (may indicate bankruptcy).

Remove clear data errors (e.g., negative totals).

Winsorize extreme values if necessary.

Document removals for audit transparency.

5. Addressing Sampling Bias / PSI
Monitor Population Stability Index (PSI).

Investigate if PSI > 0.2; resample if needed.

Ensures robust, unbiased model performance.

6. Data Normalization
Scale for Logistic Regression; skip scaling for trees.

Use ColumnTransformer to apply scaling selectively.

Avoid double-scaling to prevent mismatch.

7. Testing for Normality
Log-transform skewed ratios for Logistic Regression.

Skip transformations for tree models.

Improves calibration without overfitting.

8. Dimensionality Reduction (PCA)
Avoid PCA unless overfitting persists.

Preserve feature explainability for finance & audit purposes.

9. Feature Engineering
Focus on financial ratios and domain-driven features.

Limit arbitrary features to avoid overfitting.

Ensure SHAP compatibility for interpretability.

10. Multicollinearity Check
Use VIF (Variance Inflation Factor) > 10 as a removal threshold.

Drop redundant features to improve LR stability.

PCA/L1 regularization as fallback options.

11. Feature Selection
Correlation filtering (|r| > 0.9).

L1 regularization for Logistic Regression.

SHAP values for tree models.

Domain knowledge prioritization.

12. Hyperparameter Tuning
RandomizedSearchCV for tree models.

GridSearchCV for Logistic Regression.

Align with compute budget; monitor CV variance.

13. Cross-Validation Strategy
StratifiedKFold (k=5), shuffle enabled.

Use nested CV if computation allows.

14. Evaluation Metrics
ROC-AUC → ranking performance.

Precision-Recall AUC → focus on rare bankrupt cases.

F1-score → balance precision & recall.

Brier Score → probability calibration check.

15. Drift & Model Degradation
Monitor PSI over time; retrain if > 0.2.

Track performance metrics for early issue detection.

16. Explainability
Use SHAP for global & local feature importance.

Present top-K impactful features with concise explanations.

17. Deployment & Retraining
Retrain if PSI or key metrics drop.

Maintain model registry with version control.

Human-in-loop oversight with automated alerts.
