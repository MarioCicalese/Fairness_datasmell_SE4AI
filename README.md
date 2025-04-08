# 🔍 Exploring the Impact of Data Smells on Fairness in ML Solutions

This project investigates the relationship between **data quality issues (data smells)** and **fairness** in machine learning (ML) models. By applying various fairness metrics and bias mitigation algorithms to multiple datasets, we aim to answer critical questions regarding the ethical implications of poor data quality in AI systems.

## 🎯 Objectives

We formulated our investigation through two main **Research Questions (RQs)**:

- **RQ1:** *Does the presence of data smells impact the fairness of machine learning models?*
- **RQ2:** *Does the presence of data smells impact the performance of bias mitigation algorithms?*

By answering these questions, we aim to provide actionable insights into how data preprocessing and cleaning influence fairness in ML, and whether bias mitigation strategies remain effective under data quality issues.

---

## 📊 Datasets Used

We selected well-known datasets from the fairness literature, known to contain inherent biases:

### 1. **COMPAS**
- A recidivism prediction dataset used by the US justice system.
- **Sensitive Features:** `sex` (Privileged: Female), `race` (Privileged: Caucasian).
- **Target:** `is_recid`.

### 2. **Adult**
- U.S. census data from 1994, used to predict whether income > $50k.
- **Sensitive Features:** `sex` (Privileged: Male), `race` (Privileged: White).
- **Target:** `income`.

### 3. **Bank Marketing**
- Portuguese bank marketing data predicting term deposit subscription.
- **Sensitive Feature:** `age` (Privileged: 25 ≤ age < 60).
- **Target:** `deposit`.

> Note: We initially considered the German Credit dataset, but it was excluded due to insufficient data smells.

### ⚙️ Features and Preprocessing

- **Categorical encoding:** One-hot encoding.
- **Missing values:** Handled via imputation or removal.
- **Outliers:** Managed using Min-Max normalization and row deletion.
- **Sensitive feature encoding:** Mapped clearly for fairness metrics evaluation.

---

## 📏 Metrics and Techniques

### 🧪 Fairness Metrics
We employed **AI Fairness 360 (AIF360)** to compute:

- **SPD (Statistical Parity Difference):** Measures outcome disparity between groups.
- **AOD (Average Odds Difference):** Evaluates average difference in TPR and FPR.
- **EOD (Equal Opportunity Difference):** Assesses equality in true positive rates.
  
### 📖 Interpreting Fairness Metric Values
- **SPD (Statistical Parity Difference):**
  - A value less than 0 means the unprivileged group has a lower probability of receiving a favorable outcome compared to the privileged group.
  - A value greater than 0 indicates the opposite. A value close to 0 suggests statistical parity between groups.

- **AOD (Average Odds Difference):**
  - A value less than 0 means the unprivileged group has lower True Positive Rates (TPR) and higher False Positive Rates (FPR) compared to the privileged group.
  - A value greater than 0 indicates the reverse. A value near 0 indicates balanced error rates across groups.

- **EOD (Equal Opportunity Difference):**
  - A value less than 0 means the unprivileged group has a lower TPR, i.e., a lower chance of being correctly classified with a favorable outcome.
  - A value greater than 0 implies the privileged group has a disadvantage. Values close to 0 indicate equal opportunity.

### 🧼 Data Smell Detection
We used the **DSD (Data Smell Detection)** tool to detect issues such as:

- Duplicated Value
- Casing Inconsistencies
- Integer as Float/String
- Missing Values
- Extreme Values
- Suspect Sign

🔗 [Paper Link](https://ieeexplore.ieee.org/document/9796422) • [GitHub Tool Repository](https://github.com/mkerschbaumer/rb-data-smell-detection)
### 🧠 Models Trained
We trained standard ML classifiers:

- Decision Tree
- Support Vector Machine (SVM)
- Random Forest

### 🛡️ Bias Mitigation Algorithms
Each technique was applied on both raw and cleaned datasets:

- **Pre-processing:** `Reweighing`
- **In-processing:** `Exponentiated Gradient Reduction`
- **Post-processing:** `Equalized Odds`

---

## 🧭 Methodology

The project followed **two iterative pipelines**, one for each RQ.

### 🔁 RQ1 Pipeline
1. Select dataset.
2. Train models on **raw data**.
3. Compute fairness metrics.
4. Detect and refactor data smells.
5. Retrain on **tidy data**.
6. Recompute fairness metrics.
7. Compare and analyze results.

### 🔁 RQ2 Pipeline (extends RQ1)
1. Use same datasets/models as RQ1.
2. Apply bias mitigation algorithms to raw models.
3. Compute fairness metrics.
4. Apply bias mitigation to tidy models.
5. Recompute metrics.
6. Analyze algorithm performance under data smell conditions.

---

## 📈 Results & Analysis

### RQ1 Findings
- **Fairness metrics changed significantly** after data smells were removed.
- In most cases (COMPAS and Adult), metrics improved — i.e., moved closer to fairness (0).
- In the Bank dataset, fairness metrics **worsened**, likely due to heavy row removal (~40%).

> ✅ **Answer to RQ1:** Yes, the presence of data smells affects fairness in ML models.

### RQ2 Findings
- Bias mitigation algorithms behaved **differently** on raw vs tidy datasets.
- Performance generally **improved** on cleaned data, but some raw models with mitigation still performed competitively.
- Certain algorithms (like Equalized Odds) were more robust to data smells.

> ⚠️ **Answer to RQ2:** The results do not allow for a definitive answer. The impact of data smells on the performance of bias mitigation algorithms appears to be non-uniform and context-dependent. In some cases, algorithms performed better on tidy datasets, while in others, the presence of data smells did not significantly hinder – or even slightly improved – the metrics. Therefore, more extensive experimentation is needed to generalize any conclusion regarding this relationship.

---

## 🏁 Conclusion

This study confirms the critical role of **data quality** in achieving fair ML outcomes. Poorly managed datasets not only introduce ethical risks but can also undermine the performance of fairness-enhancing techniques.

### 🧰 Tools Used
- [AIF360 Toolkit](https://aif360.mybluemix.net/)
- DSD Tool for Data Smells
- scikit-learn for ML models
- pandas & NumPy for preprocessing
- CodeCarbon (planned): for tracking energy/CO2

---

## 📂 Repository Structure

```plaintext
📁 GermanCredit/                # Raw dataset & fairness analysis
📁 adult/            # Raw & tidy datasets + scripts for fairness analysis & bias mitigation algorithms
📁 bank/              # Raw & tidy datasets + scripts for fairness analysis & bias mitigation algorithms
📁 compas/             # Raw & tidy datasets + scripts for fairness analysis & bias mitigation algorithms
📁 docs/               # pdf documentation and pptx/pdf project presentation
📄 README.md             # This file
📄 requirements.txt            # Lists all the Python packages needed to run the project.
```
---
## 👨‍💻 Author

**Mario Cicalese**
🔗 [LinkedIn](http://www.linkedin.com/in/mario-cicalese-5b26a5283) • [GitHub](https://github.com/MarioCicalese)

**Paolo Carmine Valletta**
🔗 [LinkedIn](https://www.linkedin.com/in/paolo-carmine-valletta-4b1415279/) • [GitHub](https://github.com/PaoloCarmine1201)

**Annamaria Basile**
🔗 [LinkedIn](https://www.linkedin.com/in/annamaria-basile-2b360924a/) • [GitHub](https://github.com/Annamariabasile)
