# Credit_Risk_Scorecard
End-to-end Regulatory-Compliant Credit Scorecard development using Logistic Regression and WoE framework. Features include PD modeling, PSI/KS validation, and points-based scaling for financial risk assessment.

Credit Risk Scorecard Development 💳📊

Project Overview

This project involves the end-to-end development of a Regulatory-Compliant Credit Scorecard using the Logistic Regression and Weight of Evidence (WoE) framework. The objective is to predict the probability of default (PD) for individual customers by integrating data from Application, Behavioral, and Bureau sources.
The scorecard is scaled to a points-based system, making it easily interpretable for business stakeholders and credit officers.
________________________________________

🚀 Analytical Pipeline

1. Data Integration & Vintage Analysis

•	Data Merging: Consolidated three disparate datasets (Application, Behavioral, and Bureau) using a unique Customer_ID.
•	Target Definition: Created a Bad_Flag based on 90+ DPD (Days Past Due) logic.
•	Vintage Analysis: Calculated Months on Books (MOB) to identify a stable performance window (24 months) for model training.
•	Sampling: Data split into Training (70%), Testing (30%), and Out-of-Time (OOT) samples for validation.

2. Feature Engineering & Variable Selection

•	WoE & IV: Applied Weight of Evidence (WoE) binning to handle non-linear relationships. Used Information Value (IV) to rank predictors:
o	Strong Predictors: IV > 0.3
o	Medium Predictors: IV 0.1 to 0.3
•	Monotonicity Check: Ensured that WoE trends for selected variables follow a monotonic or nearly monotonic path to maintain logical risk consistency.
•	Multicollinearity: Utilized Variance Inflation Factor (VIF) to eliminate redundant features (VIF > 5).

3. Customer Segmentation (K-Means)

To better understand customer profiles, K-Means Clustering was implemented based on income and credit limits. This allowed for:

•	Profiling "Affluent", "Mid-market", and "High-risk" clusters.
•	Analyzing cluster-specific default rates to refine scoring logic.

4. Model Development & Scaling

•	Logistic Regression: Trained the final model on WoE-transformed variables.
•	Scorecard Scaling: Converted log-odds into a point-based system using:
o	Base Score: 600
o	Base Odds: 35/65
o	PDO (Points to Double the Odds): 50
•	Points Allocation: Each attribute bin (e.g., Age 25-30) is assigned specific points derived from model coefficients.
________________________________________

📈 Model Validation & Calibration

The model's performance was evaluated using industry-standard risk metrics:
Metric	Score	Definition
Gini Coefficient	Calculated	Measures the model's discriminatory power.
KS Statistic	Calculated	Maximum separation between 'Good' and 'Bad' distributions.
PSI	Calculated	Population Stability Index ensures the model is stable over time.
ROC-AUC	Calculated	Area under the ROC curve for overall accuracy.
Score Calibration
The final scores were calibrated using the Factor/Offset method to ensure the predicted odds match the actual observed default rates across different deciles.
________________________________________

📁 Repository Structure

•	1_Merging.py: Data cleaning and consolidation.
•	2_EDA_IV_Selection.py: Information Value and feature selection logic.
•	3_Scorecard_Model.py: Logistic Regression, WoE binning, and Scaling.
•	4_Validation.py: Gini, KS, PSI, and Rank Ordering scripts.
•	Final_Scorecard.xlsx: The readable points table for deployment.
________________________________________

🛠️ Tech Stack
•	Language: Python 3.x
•	Data Manipulation: pandas, numpy
•	Modeling/Stats: scikit-learn, statsmodels, scorecardpy
•	Visualization: matplotlib, seaborn
________________________________________

⚙️ How to Use
1.	Clone the repository.
2.	Install dependencies: pip install -r requirements.txt.
3.	Update the file paths in the scripts to point to your data source.
4.	Run the scripts sequentially from merging to validation.

