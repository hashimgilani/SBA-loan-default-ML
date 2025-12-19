# SBA Loan Default Prediction — End-to-End Machine Learning

This project applies multiple machine learning models to predict **loan default risk** using the SBA National dataset. The focus is on combining data exploration, feature engineering, model comparison, and business-driven decision rules to support real-world loan approval decisions.

The project covers the full modeling pipeline studied in the course, from exploratory analysis to profit optimization.

---

## Business Context

Banks issuing SBA-backed loans earn profits when loans are paid in full but incur significant losses when loans default.  
Because defaults are costly, the goal is not just accurate prediction, but **deciding which loans to approve** in a way that maximizes expected profit.

A loan is considered:
- **Lower risk (0)** if paid in full  
- **Higher risk (1)** if charged off  

---

## Data Exploration & Processing

The analysis begins with extensive data exploration and cleaning:

- Cleaned currency variables (loan amounts, guarantees)
- Converted `MIS_Status` into a binary **Default** indicator
- Examined class imbalance (≈70% paid in full, ≈30% default)
- Analyzed missing values and retained meaningful missingness
- Explored numeric distributions and categorical default rates

Key patterns observed:
- Smaller loans default more often
- Real estate–backed loans have lower default rates
- Default behavior varies strongly by industry and SBA guarantee portion

---

## Feature Engineering

Important predictors were constructed following course guidance:

- **Loan characteristics:** Term, Disbursement amount, SBA guarantee portion
- **Business indicators:** Number of employees, jobs created/retained
- **Binary flags:** Revolving credit, low documentation, urban location
- **Economic context:** Great Recession indicator (2008–2009)
- **Industry grouping:** First two digits of NAICS

Categorical variables were dummy encoded, numeric variables cleaned and imputed, and the final dataset prepared for modeling.

---

## Models Compared

Multiple models were trained and evaluated on validation data:

- **k-Nearest Neighbors (kNN)**
- **Single Decision Tree**
- **Bagging**
- **Random Forest**
- **XGBoost**
- **Regularized Logistic Regression**
  - LASSO
  - Ridge
  - Elastic Net
- **Neural Network (MLPClassifier)**

Each model was tuned using cross-validation and evaluated using accuracy, confusion matrices, ROC curves, and lift/gains charts.

---

## Model Performance & Selection

Across all models, **XGBoost consistently delivered the strongest performance**, with:

- Highest validation accuracy
- Strong ROC–AUC, indicating excellent ranking of risky loans
- Stable generalization compared to simpler models

Tree-based ensembles outperformed kNN and linear models, while the neural network performed competitively but did not surpass XGBoost.

---

## Profit Optimization

Rather than using a fixed probability cutoff (e.g., 0.50), the project introduces a **profit-based decision rule**:

- Approving a loan that is paid in full generates profit
- Approving a loan that defaults generates a much larger loss
- Denying a loan produces no profit or loss

By evaluating net profit across probability thresholds:

- **XGBoost produced the highest total profit**
- Maximum profit occurred when approving loans only if  
  **Predicted Probability of Default ≤ 0.15**

This threshold balances risk and return and outperforms accuracy-based rules.

---

## Business Interpretation

Key takeaways for lending decisions:

- Not all defaults are equal — ranking matters more than classification
- Aggressive approval beyond a moderate risk cutoff destroys profit
- Industry, loan size, guarantee portion, and economic conditions strongly influence default risk
- Profit-driven thresholds outperform standard classification cutoffs

This framework mirrors how real credit risk teams operate.

---

## Tools Used

- Python
- pandas, numpy
- scikit-learn
- XGBoost
- dmba utilities
- matplotlib, seaborn

---

## Key Takeaways

- End-to-end ML pipelines require more than model accuracy
- Business costs should drive decision thresholds
- Ensemble models outperform single models on complex financial data
- XGBoost provides strong accuracy, ranking power, and profitability
- Data science is most valuable when tied to real decisions

---

## Contact

- **Portfolio:** https://hashimgilani.github.io  
- **LinkedIn:** https://linkedin.com/in/syedhashimgilani  
- **Email:** hashimgilani331@gmail.com  

⭐ Thanks for checking out this SBA loan risk modeling project.
