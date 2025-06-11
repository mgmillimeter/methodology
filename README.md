
# 📘 **KDD Process — With Detailed Notes, Explanations, and Key Understandings**

---

## **1️⃣ Selection (Data Collection)**

---

### 🔹 **Identify and select relevant data sources**

✅ We used **Kaggle’s Bangladesh Student Performance EDA** dataset.
✅ Kaggle is a trusted source that provides real-world, openly accessible datasets.

💡 **Layman’s understanding:**
We need data that reflects students’ school performance as well as their family, school, and personal circumstances. Kaggle had exactly such data, so we used it.

---

### 🔹 **Define the variables of interest**

* **Dependent variable (what we want to predict):**

  * The student’s performance (scores in 5 subjects → total performance category: Low, Average, High).

* **Independent variables (factors that might affect performance):**

  * Family background, study habits, school type, access to internet, parental education, etc.

💡 **Layman’s understanding:**
We pick what "things" we believe may affect how well a student performs — these are our predictor variables.

---

### 🔹 **Extract data from databases, surveys, or other sources**

✅ We manually downloaded the dataset as a CSV file.

💡 **Layman’s understanding:**
Once we’ve identified the source, we simply grab the raw data file to work with.

---

## **2️⃣ Preprocessing (Data Cleaning)**

---

### 🔹 **Handle missing values using imputation techniques**

✅ Only 1 missing value in `location`.
✅ We filled it with the most common value ("Urban") using **mode imputation**.

💡 **Layman’s understanding:**
When information is missing, you either drop it or guess a safe value based on what's most common. Here, most students were from urban areas, so we filled the blank with "Urban".

---

### 🔹 **Identify and remove duplicate or inconsistent records**

✅ No duplicate rows found.
✅ We standardized spelling and capitalization for consistency (`Hons` → `Honors`, `urban` → `Urban`).

💡 **Layman’s understanding:**
Data often contains small spelling differences or accidental duplicates — we clean these so the computer doesn’t treat "Urban" and "urban" as two separate places.

---

### 🔹 **Detect and treat outliers to improve data quality**

✅ We used the **Interquartile Range (IQR)** rule to check for extreme values.
✅ Outliers for subject scores were kept because they represent real variation (top or weak students).
✅ Age outliers were trimmed — we kept only students aged 13–20.

💡 **Layman’s understanding:**
Sometimes there are unusually high or low values. Some make sense (high grades), but others don’t (e.g., a 2-year-old student). We kept only realistic values for our study.

---

### 🔹 **Normalize or standardize data if necessary**

✅ No normalization done.
✅ Tree-based models (Decision Tree, Random Forest) are not sensitive to scale, so we skipped this.

💡 **Layman’s understanding:**
Some models need data scaled (like SVM), but trees don’t — they just split data regardless of units or scales.

---

## **3️⃣ Transformation (Feature Engineering)**

---

### 🔹 **Convert raw data into a suitable format for analysis**

✅ Clean dataset fully organized with clear columns and categories.

💡 **Layman’s understanding:**
We prepared a nice, clean Excel-style table where every row is a student, and every column has consistent values ready for machine learning.

---

### 🔹 **Apply dimensionality reduction techniques if needed**

✅ Not applied — number of features was still manageable.

💡 **Layman’s understanding:**
If we had too many variables, we’d try to reduce them (using PCA, etc.), but we didn’t need to — 20+ features is fine.

---

### 🔹 **Encode categorical variables into numerical representations**

✅ Applied **One-Hot Encoding** for 13 categorical variables.
✅ This converts words (like "Male", "Urban") into numbers so that machine learning algorithms can process them.

💡 **Layman’s understanding:**
Computers can’t read words. So we transform words into columns of 0’s and 1’s (like "Is Male?" → Yes=1, No=0).

---

### 🔹 **Generate new derived variables that enhance analysis**

✅ Created `Total_Score` = sum of all subject scores.
✅ Created `Performance_Category` by splitting total scores into **percentiles (20th and 80th)**.

💡 **Layman’s understanding:**
We calculated each student’s total score across all subjects.
Then, instead of trying to predict raw grades, we created 3 groups:

* Top 20% = High performers
* Middle 60% = Average performers
* Bottom 20% = Low performers.

This makes classification easier and better for policy insights.

---

## **4️⃣ Data Mining (Pattern Extraction)**

---

### 🔹 **Apply statistical or machine learning techniques to extract patterns**

✅ We used **classification models**:

* Decision Tree (best performer)
* Random Forest (tested for comparison)
* Support Vector Machine (tested but weaker performance)

💡 **Layman’s understanding:**
We let machine learning algorithms "learn" how different factors lead to better or worse grades, and then predict which category each student belongs to.

---

### 🔹 **Use clustering, classification, or regression models to analyze relationships**

✅ We used classification models only.
❌ No clustering or regression needed.

💡 **Layman’s understanding:**
We already know which student is Low, Average, or High — so we train models to classify them accordingly.

---

### 🔹 **Identify trends, correlations, or predictive insights**

✅ We discovered:

* Academic track (`stu_group`) is the strongest predictor.
* Study time, attendance, extracurriculars, and parental involvement also matter.
* Commerce students are more likely to underperform if studytime is low.
* Science students generally perform better when studytime is high.

💡 **Layman’s understanding:**
The computer found that what you study, how much you study, and whether you attend class regularly are most important for predicting student success.

---

## **5️⃣ Interpretation & Evaluation (Knowledge Discovery)**

---

### 🔹 **Assess the results and validate findings**

✅ Decision Tree achieved **77.7% accuracy**.
✅ Random Forest gave similar results; SVM was less accurate.

💡 **Layman’s understanding:**
Our model correctly predicted student performance about 78% of the time — which is good for educational data, where perfect predictions are rare.

---

### 🔹 **Interpret meaningful patterns from the data**

✅ Major patterns:

* Science track + high studytime = more High performers.
* Commerce track + low studytime = more Low performers.
* Attendance and extracurricular activities have smaller effects but still helpful.

💡 **Layman’s understanding:**
These patterns tell teachers and policymakers where to focus:
Boost studytime, support weaker academic tracks, encourage extracurriculars, and improve attendance.

---

### 🔹 **Compare findings with existing research or domain knowledge**

✅ Findings match education research worldwide:

* Effort (studytime) matters most.
* School program matters (Science vs Commerce).
* Family socioeconomic status has smaller influence compared to student effort.

💡 **Layman’s understanding:**
Globally, better study habits and better academic programs consistently produce better student outcomes.

---

### 🔹 **Communicate insights through visualizations and reports**

✅ We created:

* Correlation heatmap
* Class distribution chart
* Feature importance chart
* Full decision tree visualization

💡 **Layman’s understanding:**
We turned complex data into clear pictures so readers and policymakers can easily see what matters most.

---

# 🔬 **Final Takeaway (for you as the researcher):**

* The most powerful predictors you discovered were:

  1. What academic group students belong to.
  2. How much they study.
  3. How regularly they attend school.
* Parental education, family size, internet access — important but had much smaller effects here.
* Your decision tree model is both **accurate and very easy to explain to non-technical audiences**.

---
