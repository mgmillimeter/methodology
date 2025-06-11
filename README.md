# I. INTRODUCTION
Understanding the multifactorial influences on student academic performance has become increasingly important in the context of data-driven educational research. While innate ability plays a role, numerous studies highlight the substantial impact of external factors such as socioeconomic status, parental education, school type, and access to learning resources on academic outcomes [1], [2]. These influences are particularly critical in developing countries, where systemic disparities often limit educational opportunities [3].
This study presents a multivariate analysis of socioeconomic and educational factors influencing student performance in Bangladesh. Using a structured dataset containing variables such as parental occupation and education, family size, school type, internet access, study time, attendance, tutoring, and participation in extracurricular activities, we aim to identify the most significant predictors of academic success. Performance is measured through scores in core academic subjects—English, Mathematics, Science, Social Science—and Art & Culture.
The study adopts a data-driven approach, leveraging multivariate statistical techniques to uncover patterns and correlations that traditional univariate methods may overlook. This aligns with the growing emphasis on educational data mining and learning analytics in recent literature [4], [5]. The results are expected to provide insights that inform targeted interventions and support evidence-based policymaking in educational settings, especially in low- and middle-income countries.

# II. Objectives
The primary objective of this study is to examine how socioeconomic and educational factors collectively influence student performance in the context of secondary education in Bangladesh. The research aims to explore the extent to which variables such as parental education and employment, family size, and geographic location (urban vs. rural) contribute to academic outcomes. In addition, the study investigates the impact of educational inputs, including school type, study time, internet access, tutoring, attendance, and extracurricular engagement on students' subject-specific performance across English, Mathematics, Science, Social Science, and Art & Culture.
To achieve these aims, the study employs multivariate statistical techniques to analyze the interactions between these variables and to identify the most significant predictors of student success. By leveraging a data-driven approach, the research seeks to provide empirical insights that can support evidence-based decision-making in educational policy and intervention strategies. Ultimately, the study contributes to the growing field of educational data analytics by demonstrating how multivariate analysis can be applied to real-world datasets to uncover patterns and inform educational development initiatives.



# III Methodology and Results (Full KDD-Based Rewrite)

This document presents the complete methodology and results based on the Knowledge Discovery in Databases (KDD) process, incorporating all the steps, decisions, tools, and challenges encountered. The project explores student performance classification using decision trees (J48) and association rule mining (Apriori) in WEKA.

---

## 📌 Tools Used

* **Microsoft Excel** — for data cleaning, feature creation, and category encoding
* **WEKA v3.8.6** — for building and evaluating models (J48 and Apriori)
* **WebGraphviz** — for visualizing decision trees in DOT format

---

# 📘 Step 1 – Selection (Data Collection)

This step documents the **data selection process** for the study:
**“Multivariate Analysis of Socioeconomic and Educational Factors Influencing Student Performance in Bangladesh.”**

---

## 📌 1.1 Data Source Identification

* **Source:** [Kaggle – Bangladesh Student Performance EDA](https://www.kaggle.com/code/ashikshahriar/bangladesh-student-performance-eda/input)
* **Dataset Name:** `bd_students_per.csv`
* **Format:** CSV (Comma-Separated Values)
* **Accessed by:** Manual download and upload from Kaggle to local directory
* **Type:** Structured tabular dataset
* **Purpose:** To enable multivariate analysis of how socioeconomic and educational factors influence academic outcomes among Bangladeshi secondary school students

---

## 📌 1.2 Variables of Interest

The study aims to explore the **impact of socioeconomic status, education-related inputs, and geographic factors** on student performance. Variables were selected based on their relevance to these categories.

### 🎯 Dependent Variable (Target):

* `Grade` (or disaggregated scores in English, Mathematics, Science, Social Science, and Art & Culture, if available)

### 📊 Independent Variables (Predictors):

#### ➤ Socioeconomic Factors:

* `Father_education`
* `Mother_education`
* `Father_occupation`
* `Mother_occupation`
* `Family_size`

#### ➤ Educational Factors:

* `School_type`
* `Study_time`
* `Attendance`
* `Tutoring`
* `Extracurricular`
* `Internet_access`

#### ➤ Demographic/Geographic Factors:

* `Gender`
* `Location` (Urban/Rural)

---

## 📌 1.3 Data Extraction

* The dataset was extracted from **Kaggle**, a trusted open-access data platform.
* Data likely originates from a combination of **school records** and **student/parent surveys** as implied by the Kaggle source notebook.
* The extracted file, `bd_students_per.csv`, contains all relevant variables aligned with the study objectives.
* No web scraping or third-party APIs were used in the extraction.

---



