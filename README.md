# Loan Approval Prediction Model - README

## 1. Introduction
This project investigates the feasibility of creating a loan approval prediction model that balances fairness and accuracy using recall and predictive equality as key evaluation metrics. The model examines potential biases towards or against different demographic groups, particularly in terms of race and gender.

**Research Question:**
- Can we develop a fair loan approval model that balances predictive equality and recall?
- Does this model show biases towards or against any demographic groups?

**Input Variables:**
- `Applicant Race` (C)
- `Applicant Sex` (C)
- `Loan Type` (C)
- `Property Type` (C)
- `Loan Purpose` (C)
- `Loan Amount` (N)
- `Applicant Income` (N)

**Output Variable:**
- `Action Taken` (C) - Indicates whether a loan was approved or denied.

**Evaluation Metrics:**
- **Recall**: Prioritizing false negatives (approved applicants being denied).
- **Predictive Equality**: Ensuring equal treatment across demographic groups.
- **Statistical Parity & Calibration**: Additional fairness considerations.

---

## 2. Dataset Information
The dataset used in this project is from the **Consumer Financial Protection Bureau (CFPB)** and contains mortgage application data. The dataset comprises **9,793,702 rows** and **29 columns**, covering various attributes related to loan applications.

**Key Columns Used:**
- `loan_type`: Type of loan applied for.
- `property_type`: Type of property associated with the loan.
- `loan_purpose`: Purpose of the loan.
- `loan_amount_000s`: Loan amount in thousands.
- `applicant_income_000s`: Applicant’s annual income in thousands.
- `applicant_race_1`: Race of the applicant.
- `applicant_sex`: Gender of the applicant.
- `action_taken`: Loan application outcome.

**Data Source:**
- **CFPB HMDA Data** ([Link](https://www.consumerfinance.gov/data-research/hmda/historic-data/?geo=nationwide&records=all-records&field_descriptions=codes))
- The dataset is mandated by the **Home Mortgage Disclosure Act (HMDA)** and is publicly available.

---

## 3. Preprocessing Steps
### Steps Taken:
1. **Column Selection:** Removed irrelevant columns (e.g., `application_date_indicator`).
2. **Handling Missing Data:** Dropped columns with **>30% missing values**.
3. **Row Filtering:** Removed non-2017 data and entries where sex ≠ 1 or 2.
4. **Categorical Encoding:** Applied **Label Encoding** to categorical variables.
5. **Balancing the Dataset:** Used **undersampling** for racial and gender fairness comparisons.

**Final Processed Data:** Stored as `cleaned_data.csv`.

---

## 4. Modeling Approaches
### Models Used:
1. **Logistic Regression** (Baseline Model)
2. **K-Nearest Neighbors (KNN)**
3. **Random Forest Classifier**
4. **Balanced KNN (with downsampling)**
5. **Balanced Random Forest (with downsampling)**

### Data Splitting:
- **Training Set:** 67% of data
- **Test Set:** 33% of data

### Fairness Evaluation:
- **False Positive Rate (FPR)**: Measures incorrectly approved loans.
- **False Negative Rate (FNR)**: Measures incorrectly denied loans.
- **Predicted Positive Rate (PPR)**: Measures overall loan approval likelihood.

---

## 5. Results and Analysis
### General Observations:
- **Baseline models (Logistic, KNN, RF) had ~60% accuracy.**
- **Balanced models improved to ~78% accuracy**, showing better fairness outcomes.
- **False Positive Rates were higher for males & white applicants**, indicating systemic bias.
- **Downsampling improved fairness**, reducing disparities across demographic groups.

### Performance By Gender:
| Model | Male Recall | Female Recall | Male FPR | Female FPR |
|-------|------------|--------------|---------|---------|
| Logistic Regression | 60% | 59% | 32% | 28% |
| KNN | 61% | 62% | 33% | 29% |
| Random Forest | 62% | 60% | 34% | 30% |
| Balanced KNN | 65% | 73% | 44% | 33% |
| Balanced RF | 78% | 82% | 30% | 17% |

### Performance By Race:
| Model | White Recall | Black Recall | Asian Recall | NH/PI Recall |
|-------|------------|--------------|-------------|--------------|
| Logistic Regression | 61% | 58% | 54% | 61% |
| KNN | 62% | 59% | 55% | 62% |
| Random Forest | 63% | 60% | 56% | 63% |
| Balanced KNN | 65% | 78% | 66% | 79% |
| Balanced RF | 80% | 83% | 78% | 85% |

**Key Takeaways:**
- **Baseline models show systemic bias favoring men & white applicants.**
- **Balanced models reduce bias but still show disparities.**
- **False positive rates favor men and white applicants, leading to better financial opportunities for these groups.**

---

## 6. Conclusion and Limitations
### Conclusions:
- **Balanced Random Forest performed best (~78% accuracy).**
- **Bias remains** in favor of **men and white applicants** despite dataset balancing.
- **False positives (incorrect approvals) favor men & white applicants**, highlighting financial disparities.

### Limitations:
1. **Computational Constraints:** Model training was limited due to hardware.
2. **Binary Gender Classification:** Does not account for non-binary individuals.
3. **Simplified Loan Approval Outcomes:** Only `originated` was considered instead of other nuanced categories.
4. **No Credit Score Data:** Missing a key predictor of loan approval likelihood.

---

## 7. References
1. Investopedia: [5 Steps to Scoring a Mortgage](https://www.investopedia.com/articles/mortgages-real-estate/08/mortgage-candidate.asp)
2. Lee & Yang (2023): [Fair Credit Risk Predictions](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4602450)
3. Women’s World Banking (2021): [Algorithmic Bias in Financial Inclusion](https://www.womensworldbanking.org/wp-content/uploads/2021/02/2021_Algorithmic_Bias_Report.pdf)
4. CFPB: [HMDA Data Overview](https://www.consumerfinance.gov/data-research/hmda/)
5. Federal Trade Commission: [Gramm-Leach-Bliley Act](https://www.ftc.gov/business-guidance/resources/how-comply-privacy-consumer-financial-information-rule-gramm-leach-bliley-act)

