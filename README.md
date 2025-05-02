# GWU_RML Group 6

## Person or Organization Developing Model
- Apoorva Paranthaman (apoorvap@abc.edu)
- Maryam Shahbaz Ali (maryamshahba.a@abc.edu)
- Zahra Sultani (zahrasultai@abc.edu)

## Model Information
- **Model Date:** May 2025
- **Model Version:** 1.0
- **License:** Apache License

## Intended Use
### Value of Best Remediated Model
The remediated model, based on data from the Home Mortgage Disclosure Act (HMDA), is designed solely for educational purposes. It tests for biases between men and women, as well as races such as black vs. white and other demographic categories in the dataset. The primary goal of this model is to serve as a learning tool for students to understand and practice identifying and addressing biases in data. This model is not built to resolve a real-world problem. However, by engaging in such practices in a similar real-world project, a remediated model can help the project achieve some of the following potential values:
-	**Market-Leading Status:** Enhances reputation through fair lending practices.
-	**Obligations to Lenders/Creditors:** Ensures compliance with fair lending laws.
-	**Shareholder Returns:** Reduces legal risks and improves customer satisfaction.
-	**Profitability:** Identifies profitable, unbiased lending opportunities.
-	**Sustainability:** Builds trust and loyalty among diverse customers.
-	**Growth Prospects:** Opens new market segments through fair criteria.

### How to Use the Best Remediated Model 
The best remediated model is used for assessing bias and can be used for the following purposes:
- **Intended Scope:** Use for assessing and mitigating biases in mortgage lending.
- **Capabilities and Limitations:** Understand its ability to detect and correct biases.
- **Appropriate Application:** Apply consistently across all demographic groups.
- **Monitoring and Validation:** Regularly check for and adjust new biases.
- **Regulatory Compliance:** Adhere to fair lending laws (ECOA, FHA).
- **Stakeholder Communication:** Ensure transparency with regulators, lenders, and customers.

### Primary Intended Users
- Students in GWU DNSC_6330 class

### Additional Purposes
- This model is an educational example and cannot be used for any additional purposes.

## Training Data
- **Source of Training Data:** The training data is from the Home Mortgage Disclosure Act (HDMA) and was downloaded from the class’s repository: [GWU_rml Data](https://github.com/jphall663/GWU_rml/tree/3860843bd60a785452c5dd1cffa522240ea47d82/assignments/data)
- **Training and Validation Split:** 70% training and 30% test.
- **Number of Rows in Training:** 112,253

### Data Dictionary
| Column Name                     | Type   | Measurement Level | Description                                                                 |
|---------------------------------|--------|-------------------|-----------------------------------------------------------------------------|
| High_pried                      | Target | Int               | Target variable indicating whether the mortgage loan is high-priced         |
| term_360                        | Input  | Int               | Indicates whether the mortgage term is 360 months (1) or other types (0)    |
| conforming                      | Input  | Int               | Indicates whether the mortgage conforms to normal standards (1) or not (0)  |
| debt_to_income_ratio_missing    | Input  | Int               | Indicates whether the debt-to-income ratio is missing                       |
| loan_amount_std                 | Input  | Float             | Standardized loan amount of the mortgage for each applicant                 |
| loan_to_value_ratio_std         | Input  | Float             | Standardized loan-to-value ratio indicating the ratio of the mortgage size to the value of the property for each applicant |
| no_intro_rate_period_std        | Input  | Float             | Standardized indicator for no introductory rate period                      |
| intro_rate_period_std           | Input  | Float             | Standardized introductory rate period                                       |
| property_value_std              | Input  | Float             | Standardized property value                                                 |
| income_std                      | Input  | Float             | Standardized income for each applicant                                      |
| debt_to_income_ratio_std        | Input  | Float             | Standardized debt-to-income ratio                                           |

### Engineered Columns
| Column Name | Type        | Measurement Level | Description                                                                 |
|-------------|-------------|-------------------|-----------------------------------------------------------------------------|
| race        | Target      | Int               | A combined race column created from individual race indicators (black, Asian, white, other) |
| male        | demographic info | Int             | whether a person identifies as male (1) or not male (0)                                     |
| female        | demographic info | Int             | whether a person identifies as female (1) or not female (0)                                     |
| High_priced | Target      | Int               | Target variable indicating whether the mortgage loan is high-priced         |

## Evaluation Data
- **Source of Test Data:** The test data is from the Home Mortgage Disclosure Act (HDMA) and was downloaded from the class’s repository: [GWU_rml Data](https://github.com/jphall663/GWU_rml/tree/3860843bd60a785452c5dd1cffa522240ea47d82/assignments/data)
- **Number of Rows in Test Data:** 48,085
- **Difference in Columns Between Training and Test Data:** The 'high_priced' column is excluded from test data.

## Model Details
- **Columns Used as Inputs:** `x_names = ['term_360', 'conforming', 'debt_to_income_ratio_missing', 'loan_amount_std', 'loan_to_value_ratio_std', 'no_intro_rate_period_std', 'intro_rate_period_std', 'property_value_std', 'income_std', 'debt_to_income_ratio_std']`
- **Columns Used as Targets:** `y_name = 'high_priced'`
- **Type of Model:** Explainable Boosting Machine (EBM) model.
- **Software Used:** Python’s interpret library including 'xgboost', 'H2O', 'pd', and 'np'.
- **Version of Modeling Software:**
  - Interpret (0.6.10)
  - xgboost (2.1.4)
  - h2o (2.0.2)
  - pd (2.2.2)
  - numpy (2.0.2)

### Hyperparameters
```python
# Best remediated params from assignment 3
rem_params = {
    'max_bins': 256,
    'max_interaction_bins': 16,
    'interactions': 15,
    'outer_bags': 8,
    'inner_bags': 4,
    'learning_rate': 0.05,
    'validation_size': 0.1,
    'min_samples_leaf': 10,
    'max_leaves': 3,
    'n_jobs': 4,
    'early_stopping_rounds': 100,
    'random_state': 10001
}
```
## Quantitative Analysis
### AIR Summary Table for Each Demographic Group with Remediated EBM Predictions
| Compare vs. Control | AIR   |
|---------------------|-------|
| Asian vs. White     | 1.140 |
| Black vs. White     | 0.855 |
| Females vs. Males   | 0.948 |

*Table 1. Validation AIR values for race and sex groups.*

See the full EBM notebook with code on GitHub for details of quantitative analysis.

### Metrics Used to Evaluate the Best Remediated Model
The metrics used are AUC (Area Under the Curve) and F1-score, installed from `interpret.perf` and `sklearn.metrics` packages.

### Values of the Metrics for Training, Validation, and Evaluation Data
Models were assessed primarily with AUC and AIR. See details below:

| Train AUC | Validation AUC | Test AUC |
|-----------|----------------|----------|
| 0.7374    | 0.8250         | 0.831*   |

*Table 2. AUC values across data partitions.*

*The test AUC value is taken from [model_eval_2025_03_27_14_06_12.csv](https://github.com/jphall663/GWU_rml/blob/3860843bd60a785452c5dd1cffa522240ea47d82/assignments/model_eval_2025_03_27_14_06_12.csv).*

### Plots for the Best Remediated Model
#### Basic Data Exploration
 <p align="center">
    <img src="Images/heatmap for correlations_basic data exploration.png" width="400">
</p>
*Figure 1: Heatmap showing the correlation between different features, which helps in identifying relationships and dependencies among the features. See full notebook [here](link_to_notebook).*

#### Partial Dependence for Top 3 Most Important Variables in EBM Model
 <p align="center">
    <img src="Images/PD loan to value ratio std.png" width="200"><img src="Images/PD property value std.png" width="200"><img src="Images/PD debt to income ratio std.png" width="200"><img src="Images/PD Intro rate period std.png" width="200">
</p>
*Figure 2: Best EBM Partial Dependence for top 4 features; 'loan_to_value_ratio_std', 'property_value_std', 'debt_to_income_ratio_std', and 'intro_rate_period_std', using the Explainable Boosting Machine model, showing the relationship between those features and the model's predictions. See full notebook [here](link_to_notebook).*

 <p align="center">
    <img src="Images/Best EBM Feature Importance_EBM only.png" width="300">
</p>
*Figure 3: The global feature importance for the EBM model, showing the significance of features, which helps in understanding which features are most influential in the model's predictions. Based on this plot, 'loan_to_value_ratio_std', 'property_value_std', 'debt_to_income_ratio_std' have the highest importance for the model. See full notebook [here](link_to_notebook).*

 <p align="center">
    <img src="Images/DT Updated for Assignment 4.png" width="700">
</p>
*Figure 4: The stolen decision tree model extracts stolen tree as an adversarial example attack, which allowed identifying vulnerabilities in the model's decision-making process. The stolen model was used to find the low and high adversary seed rows for adversary searches. See the full notebook [here](link_to_notebook).*

 <p align="center">
    <img src="Images/Variable importance for stolen model.png" width="400">
</p>
*Figure 5: Variable Importance for H2O Distributed Random Forest highlighting the importance of features for the stolen model.*

 <p align="center">
    <img src="Images/Global Logloss Residuals.png" width="300">
</p>
*Figure 6: The Residuals analysis shows if the model struggles to predict when customers will receive a high-priced loan correctly. It does much better when predicting customers will NOT receive a high-priced loan. There are also some very noticeable outliers. Full notebook [here](link_to_notebook).*

 <p align="center">
    <img src="Images/ICE Plot for Feature Index 0.png" width="300">
</p>
*Figure 7: The individual conditional expectation (ICE) curves for Feature Index 0. Each line represents the partial dependence of the model's prediction on the feature value for a single instance. See full notebook [here](link_to_notebook).*

### Address Other Alternative Models Considered
 <p align="center">
    <img src="Images/Local feature across models.png" width="600">
</p>
*Figure 8: Some other models include GLM and Monotonic XGBoost model and the local feature importance has been compared across models in 10th, 50th, and 90th Percentile. See full notebook [here](link_to_notebook).*

## Ethical Considerations
### Potential Negative Impacts of Using the Best Remediated Model
- **Biases:** Even with remediation, this model can still exhibit biases such as bias in algorithms or training data. Models might perform well on training data but fail to generalize unseen data, leading to inaccurate predictions in real-world.
- **Model Drift:** Over time, the model’s performance can drift due to changes in the data distribution, necessitating monitoring updates.
- **Unfair Decisions:** The model’s decisions could lead to unfair loan approvals and affect individuals resulting in discrimination in real-world situations.

### Potential Uncertainties Relating to the Impacts of Using the Best Remediated Model
- **Uncertainty in Model Performance:** Despite remediation, there is always uncertainty regarding how well the model will perform in diverse real-world scenarios. Unexpected events such as recession and outbreaks affect model performance.
- **Software Bugs:** Unforeseen bugs or vulnerabilities in software implementation can lead to incorrect model outputs or security risks.
- **Legal Complications:** The model might behave unpredictably when exposed to new types of data or adversarial examples, leading to unintended consequences such as legal penalties.

### Unexpected Results Encountered During Training
- After fitting the EBM model, the calculated model AUC turned out to be 1, which is not possible in real-world scenarios.

## Explanation of Some Functions and Processes
- **get_max_f1_frame:** This function calculates the optimal cutoff for the model based on the F1 score.
- **get_confusion_matrix:** This function generates confusion matrices for different demographic groups.
- **air:** This function calculates the Adverse Impact Ratio (AIR) for different demographic groups.
