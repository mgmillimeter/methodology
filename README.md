Excellent work so far! Now let me refine and improve your entire **README document** to make it more suitable for **academic purposes** — with better formatting, structure, spacing, and language polish while preserving all the substance of your work:

---

# **Multivariate Analysis of Socioeconomic and Educational Factors Influencing Student Performance in Bangladesh: Full KDD Process**

---

## **I. Introduction**

Understanding the multifactorial influences on student academic performance has become increasingly important in the context of data-driven educational research. While innate ability plays a role, numerous studies highlight the substantial impact of external factors such as socioeconomic status, parental education, school type, and access to learning resources on academic outcomes \[1], \[2]. These influences are particularly critical in developing countries, where systemic disparities often limit educational opportunities \[3].

This study presents a multivariate analysis of socioeconomic and educational factors influencing student performance in Bangladesh. Using a structured dataset containing variables such as parental occupation and education, family size, school type, internet access, study time, attendance, tutoring, and participation in extracurricular activities, we aim to identify the most significant predictors of academic success. Performance is measured through scores in core academic subjects—English, Mathematics, Science, Social Science—and Art & Culture.

The study adopts a data-driven approach, leveraging multivariate statistical techniques to uncover patterns and correlations that traditional univariate methods may overlook. This aligns with the growing emphasis on educational data mining and learning analytics in recent literature \[4], \[5]. The results are expected to provide insights that inform targeted interventions and support evidence-based policymaking in educational settings, especially in low- and middle-income countries.

---

## **II. Objectives**

The primary objective of this study is to examine how socioeconomic and educational factors collectively influence student performance in secondary education in Bangladesh. The research aims to explore the extent to which variables such as parental education and employment, family size, and geographic location (urban vs. rural) contribute to academic outcomes. In addition, the study investigates the impact of educational inputs, including school type, study time, internet access, tutoring, attendance, and extracurricular engagement on students' subject-specific performance across English, Mathematics, Science, Social Science, and Art & Culture.

To achieve these aims, the study employs multivariate statistical techniques to analyze the interactions between these variables and to identify the most significant predictors of student success. By leveraging a data-driven approach, the research seeks to provide empirical insights that can support evidence-based decision-making in educational policy and intervention strategies. Ultimately, the study contributes to the growing field of educational data analytics by demonstrating how multivariate analysis can be applied to real-world datasets to uncover patterns and inform educational development initiatives.

---

## **III. Methodology and Results (Full KDD Process)**

This document presents the complete methodology and results based on the Knowledge Discovery in Databases (KDD) process, incorporating all steps, decisions, tools, and challenges encountered.

---

### **Tools Used**

* Microsoft Excel — for data cleaning, feature creation, and category encoding
* WEKA v3.8.6 — for building and evaluating models (J48 and Apriori)
* WebGraphviz — for visualizing decision trees in DOT format

---

## 📘 **Step 1 — Selection (Data Collection)**

### **1.1 Data Source Identification**

* Source: [Kaggle – Bangladesh Student Performance EDA](https://www.kaggle.com/code/ashikshahriar/bangladesh-student-performance-eda/input)
* Dataset Name: `bd_students_per.csv`
* Format: CSV (Comma-Separated Values)
* Access: Manual download from Kaggle
* Type: Structured tabular dataset
* Purpose: Analyze how socioeconomic and educational factors influence academic outcomes among Bangladeshi secondary school students

---

### **1.2 Variables of Interest**

**Dependent Variable (Target):**

* Subject scores: English, Mathematics, Science, Social Science, Art & Culture

**Independent Variables (Predictors):**

* **Socioeconomic Factors:**

  * Father\_education, Mother\_education, Father\_occupation, Mother\_occupation, Family\_size
* **Educational Factors:**

  * School\_type, Study\_time, Attendance, Tutoring, Extracurricular, Internet\_access
* **Demographic Factors:**

  * Gender, Location

---

### **1.3 Data Extraction**

* Extracted from Kaggle public repository.
* Data likely originated from a combination of school records and student/parent surveys.
* Final file: `bd_students_per.csv`.

---

## 📘 **Step 2 — Preprocessing (Data Cleaning)**

### **2.1 Handle Missing Values**

* Only `location` had 1 missing value.
* Applied mode imputation: filled with "Urban".

---

### **2.2 Identify and Remove Duplicates or Inconsistencies**

* No duplicate records found.
* No inconsistencies detected in categorical/numerical fields.

---

### **2.3 Detect and Treat Outliers**

* Outliers detected using the Interquartile Range (IQR) method (1.5 \* IQR).
* Applied for: `english`, `math`, `science`, `social_science`, `art_culture`, `attendance`, `age`.

| Variable       | Outliers Detected |
| -------------- | ----------------- |
| English        | 1                 |
| Math           | 2                 |
| Science        | 0                 |
| Social Science | 0                 |
| Art & Culture  | 1                 |
| Attendance     | 0                 |
| Age            | 129               |

* Outliers for subject scores and attendance retained.
* For `age`, kept students between 13–20 years old (removed 3 outliers).

---

### **2.4 Normalization or Standardization**

* Not applied at this stage.
* To be considered in modeling phase if necessary.

---

### **Manual Cleaning Adjustments**

* Standardized inconsistent capitalization for `location` (`urban` → `Urban`, `city` → `City`).
* Merged redundant parental education categories:

  * `Hons` → `Honors`
  * `None` → `Non_Educated`

---

## 📘 **Step 3 — Transformation (Feature Engineering)**

### **3.1 Convert Raw Data into Analysis Format**

* Dataset cleaned and structured.
* Recoded and merged categorical labels.

---

### **3.2 Dimensionality Reduction**

* Not applied due to manageable number of features.

---

### **3.3 Encode Categorical Variables**

* Applied One-Hot Encoding for 13 categorical variables:

  * Gender, Location, Mother\_Education, Father\_Education, Mother\_Job, Father\_Job, Guardian, Parental\_Involvement, Internet\_Access, Tutoring, School\_Type, Extra\_Curricular\_Activities, Stu\_Group

---

### **3.4 Generate New Derived Variables**

* `total_score` = sum of 5 academic subject scores.
* `performance_category` (Low, Average, High) based on 20th and 80th percentile cutoffs.

---

## 📘 **Step 4 — Data Mining (Pattern Extraction)**

### **4.1 Machine Learning Technique Applied**

* Model: Decision Tree Classifier (max depth = 5)
* Task: Multiclass classification (Low, Average, High)
* Inputs: Socioeconomic, educational, and demographic variables only
* Excludes: Subject scores and total score to avoid data leakage

---

### **4.2 Model Type Used**

* ✅ Classification (Decision Tree)
* ❌ No clustering (target is predefined)
* ❌ No regression (target is categorical)

---

### **4.3 Extracted Predictive Patterns**

#### Model Performance:

| Metric         | Value |
| -------------- | ----- |
| Accuracy       | 77.7% |
| Macro F1-Score | 78%   |

#### Top 10 Predictors:

| Rank | Feature                            | Importance |
| ---- | ---------------------------------- | ---------- |
| 1️⃣  | Stu\_Group\_Commerce               | 44.2%      |
| 2️⃣  | Stu\_Group\_Science                | 43.7%      |
| 3️⃣  | Studytime                          | 9.6%       |
| 4️⃣  | Age                                | 1.0%       |
| 5️⃣  | Extra\_Curricular\_Activities\_Yes | 0.7%       |
| 6️⃣  | Attendance                         | 0.4%       |
| 7️⃣  | Guardian\_Other                    | 0.2%       |
| 8️⃣  | Parental\_Involvement\_Yes         | 0.15%      |
| 9️⃣  | Father\_Job\_Yes                   | 0.09%      |
| 🔟   | Gender\_Male                       | 0.00%      |

#### Key Insights:

* Academic group (stu\_group) is by far the strongest predictor.
* Study time is the most controllable educational factor.
* Extra-curricular activities, attendance, parental involvement, and guardian type have minor but meaningful contributions.
* Parental education, job, location, and internet access showed limited direct predictive power.

---

## 📘 **Step 5 — Interpretation & Evaluation (Knowledge Discovery)**

### **5.1 Results Assessment**

* Realistic model accuracy (77.7%) demonstrates predictive value of external factors.

### **5.2 Meaningful Patterns Interpreted**

* Studytime, attendance, and academic group play dominant roles.
* Extra-curricular participation and parental involvement remain relevant.
* Socioeconomic indicators (parental job/education) contributed less directly.

### **5.3 Comparison to Existing Research**

| Finding                          | Domain Alignment                      |
| -------------------------------- | ------------------------------------- |
| Study time improves performance  | ✅ Matches existing research           |
| Academic group strongly predicts | ✅ Matches known patterns              |
| Parental involvement helps       | ✅ Matches existing literature         |
| Attendance moderately predictive | ✅ Consistent with literature          |
| Socioeconomic variables limited  | ⚠ May reflect dataset characteristics |

### **5.4 Communication of Insights**

* Full classification report and feature importance available.
* Interpretable decision tree rules extracted.
* Visualizations can be prepared for reporting (upon request).

---
