# Predicting Patient Complication Risk Using Random Forest Classification

---

# Executive Summary

This report presents the results of a predictive modeling study conducted to evaluate whether structured categorical health indicators can accurately classify patient complication risk into Low, Medium, or High categories.

Using a Random Forest classification approach, we analyzed a reduced feature set consisting of ten binary medical condition indicators. The objective was to determine whether commonly recorded comorbidities provide sufficient discriminatory signal for risk stratification.

Findings indicate that the selected features do not provide adequate predictive power. Model performance remained near baseline levels even after systematic hyperparameter tuning. These results suggest that additional clinical, behavioral, and longitudinal variables are required to support reliable complication risk prediction.

The primary conclusion of this study is that feature richness—not algorithm complexity—is the limiting factor in this predictive framework.

---

# 1. Background and Organizational Context

Healthcare systems face increasing operational and financial pressure to proactively manage patient risk. Accurate early identification of complication risk supports:

* Targeted clinical interventions
* Resource allocation planning
* Reduction of preventable adverse events
* Improved patient outcome management

This study investigates whether structured intake indicators alone can support effective risk classification.

---

# 2. Research Objective

To evaluate whether ten categorical health indicators can predict patient complication risk categorized as:

* Low (0)
* Medium (1)
* High (2)

The broader objective is to assess whether existing structured medical condition data is sufficient for predictive modeling without incorporating laboratory values, treatment intensity metrics, or longitudinal clinical history.

---

# 3. Dataset Overview

The dataset contains 10,000 patient records and 50 variables. For this analysis, a focused subset of categorical health indicators was selected.

## Independent Variables

* Overweight
* HighBlood
* Stroke
* Arthritis
* Hyperlipidemia
* BackPain
* Anxiety
* AllergicRhinitis
* RefluxEsophagitis
* Asthma

## Dependent Variable

* ComplicationRisk (Low, Medium, High)

All predictors are binary categorical variables.

---

# 4. Data Preparation and Processing

## Column Standardization

Column names were normalized to ensure consistency across the modeling pipeline.

## Feature Selection

A reduced feature set was intentionally chosen to isolate the predictive contribution of core health conditions.

## Encoding Strategy

* Independent variables encoded using OrdinalEncoder (No = 0, Yes = 1)
* Target variable encoded using LabelEncoder (Low = 0, Medium = 1, High = 2)

No missing values or duplicate records required remediation.

---

# 5. Modeling Methodology

## Model Selection

Random Forest classification was selected due to:

* Robustness to overfitting
* Stability across heterogeneous categorical predictors
* Interpretability via feature importance
* Resistance to noise and outliers

The model uses bootstrap aggregation to build multiple decision trees and aggregates predictions via majority voting. Class probabilities were generated using predict_proba().

---

# 6. Baseline Model Results

Initial model evaluation on the test dataset produced the following results:

* Accuracy: 34.4%
* Macro F1 Score: 0.337
* Macro AUC-ROC: 0.5028

Confusion matrix analysis revealed high misclassification across all three complication risk categories, with limited separation between classes.

Performance was only marginally better than random classification.

---

# 7. Hyperparameter Optimization

Stratified 5-fold cross-validation was used to tune:

* n_estimators
* max_depth
* min_samples_split
* min_samples_leaf
* max_features

Optimization metric: Macro F1-score

Despite systematic tuning, model performance improved only marginally.

---

# 8. Optimized Model Results

* Accuracy: 34.6%
* Macro Precision: 0.339
* Macro Recall: 0.338
* Macro F1 Score: 0.334
* AUC-ROC: Approximately 0.50 across classes

The optimized model demonstrated no meaningful improvement over the baseline model.

---

# 9. Interpretation of Findings

The limited predictive performance suggests that the selected health indicators do not provide sufficient discriminatory signal for multi-class complication risk stratification.

The model’s performance plateau indicates that algorithm selection is not the primary constraint. Instead, the predictive ceiling appears driven by limited feature depth.

Risk classification likely requires:

* Continuous clinical measurements
* Laboratory results
* Treatment intensity metrics
* Length of stay variables
* Demographic interaction effects
* Longitudinal patient history

---

# 10. Limitations

* Restricted to ten categorical comorbidity indicators
* No continuous clinical data
* No laboratory values
* No service intensity metrics
* No temporal patient history
* No feature interaction engineering

These limitations constrain the model’s ability to meaningfully differentiate risk levels.

---

# 11. Recommendations

The current model should not be deployed in a clinical decision-support environment.

Recommended next steps:

1. Expand feature collection to include continuous clinical indicators
2. Incorporate hospitalization metrics (Initial_days, TotalCharge, Services)
3. Integrate laboratory values and medication data
4. Explore gradient boosting methods once feature expansion is complete
5. Conduct feature importance analysis after dataset enrichment

---

# 12. Conclusion

This study demonstrates that categorical comorbidity indicators alone are insufficient for reliable complication risk prediction.

The primary organizational insight is that predictive performance in healthcare analytics is fundamentally dependent on data richness. Without clinically informative features, even robust ensemble methods cannot produce reliable stratification.

Future modeling efforts should prioritize feature expansion before pursuing algorithmic complexity.
