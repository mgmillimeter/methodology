# 📘 Methodology and Results (README Format)

This document outlines the full step-by-step process for analyzing student performance using WEKA and Excel. It follows the Knowledge Discovery in Databases (KDD) process, from data preparation to modeling and discussion.

---

## 📌 Tools Used

* **Microsoft Excel** — for data cleaning, transformation, and feature engineering
* **WEKA v3.8.6** — for classification (J48 decision tree) and association rule mining (Apriori)
* **WebGraphviz** — for visualizing the decision tree

---

## 🔍 Step-by-Step Process

### 🔹 1. Initial Review (Excel)

**Goal:** Understand the raw dataset structure

* Opened `bd_students_per_uncleaned.csv` in Excel
* Inspected for formatting issues, irrelevant columns, and text inconsistencies
* Identified 24 attributes including scores and socio-demographics

### 🔹 2. Data Cleaning (Excel)

| Task                    | Action Taken                                           | Why It Matters                                     |
| ----------------------- | ------------------------------------------------------ | -------------------------------------------------- |
| Removed columns         | Deleted `id` and `full_name`                           | Irrelevant for analysis                            |
| Removed duplicates      | Excel's `Remove Duplicates` → 315 rows removed         | Prevent bias due to repeated data                  |
| Fixed missing value     | 1 row with missing `location` deleted                  | Incomplete data affects model reliability          |
| Fixed capitalization    | Replaced `urban`/`city` with `Urban`/`City`            | Prevents WEKA from reading duplicates as different |
| Standardized categories | Cleaned inconsistent strings (e.g., `hons` → `Honors`) | Ensures consistency                                |
| Fixed attribute names   | Renamed corrupted headers (e.g., `Ã¥ge` → `age`)       | Prevents WEKA errors                               |

### 🔹 3. Feature Engineering (Excel)

* Created `overall_avg_score` (average of 5 subjects)
* Created `performance_category` (Low/Medium/High) using percentiles:

```excel
=IF(X2<=69.4, "Low", IF(X2<=80.2, "Medium", "High"))
```

### 🔹 4. Dataset Finalization (Excel)

* Ensured all attributes were correctly labeled and cleaned
* Saved as `cleaned_bd_students.csv`

---

## ⚙️ WEKA Analysis

### 🔹 5. Load and Setup

* Opened `cleaned_bd_students.csv` in WEKA → **Preprocess tab**
* Set `performance_category` as the **class attribute**

### 🔹 6. Discretization (for Apriori only)

* Applied: `Filters → Unsupervised → Attribute → Discretize`
* Transformed numerical data into 3 bins (Low, Medium, High)

### 🔹 7. J48 Decision Tree

* Classifier: `trees → J48`
* Evaluation method: `10-fold cross-validation`
* **Accuracy:** ✅ **96.08%**

#### 🌳 Key Rules Found:

* `stu_group = Science` AND `studytime > 5` → High
* `stu_group = Arts` AND `studytime <= 3.5` → Low
* `attendance > 91` boosts outcomes even with lower studytime

#### ⚠️ Visualization Challenge:

* WEKA doesn’t export tree diagrams
* Solution: copied tree text → pasted into [WebGraphviz](https://webgraphviz.com)

### 🔹 8. Apriori Association Rule Mining

* Menu: `Associations → Apriori`
* Settings: support ≥ 0.3, confidence ≥ 0.9
* **Top Rules:**

  * `stu_group = Arts` AND `studytime = Low` → `performance = Low` (99% confidence)
  * `stu_group = Science` AND `studytime = High` → `performance = High` (98–99% confidence)

---

## 📈 Results and Discussion

### 📌 Decision Tree (J48)

The J48 decision tree achieved high accuracy (96.08%) and revealed clear top-level decision factors:

* Academic track (`stu_group`)
* Daily study time
* Attendance

These variables alone allowed the tree to classify students accurately into Low, Medium, or High performers.

**Why the Top 3 Levels Matter:**

* They split the data into large, meaningful categories
* Deeper levels only apply to small subgroups
* This simplification aligns with the objective of providing actionable insights for educators

### 📌 Apriori Complement

Apriori helped validate and **complement** the J48 tree by showing **frequent, high-confidence patterns**:

* Unlike J48’s structure, Apriori shows general trends across the entire dataset
* It confirmed key combinations that commonly lead to poor or good performance

Together:

* **J48** = how to classify performance
* **Apriori** = what combinations lead to certain outcomes

This dual method supports your objective of understanding student performance **and offering practical guidance** to schools.

---

## ✅ Summary of Tools & Why We Used Them

| Tool            | Role                        | Reason                                            |
| --------------- | --------------------------- | ------------------------------------------------- |
| **Excel**       | Cleaning and engineering    | Fast, visual control for string/text-based fixes  |
| **WEKA**        | Modeling and pattern mining | Accessible tool with strong classifiers and rules |
| **WebGraphviz** | Decision tree visualization | Converts WEKA output into readable tree diagrams  |

---

## ✅ Conclusion

By combining J48 and Apriori, we gained both **predictive models** and **descriptive insights**. These results can support schools in identifying at-risk students and applying interventions based on:

* Group (Arts, Science, Commerce)
* Study habits
* Attendance and family background

The approach followed here is explainable, data-driven, and practical — suitable for educational settings and easy to replicate using free tools.

---
