# 📊 Exploratory Data Analysis Summary - HRA Records Dataset

## Description:
An **HRA (Human Resources Analytics)** dataset containing over **5 million records** is retrieved from a **SQL Server database** using **PyODBC**. After ingestion, the data is converted to **Spark DataFrame** for further exploration and computation. This approach is particularly useful in environments where raw data in databases is often protected and cannot be altered or explored directly. Instead, we pull the data into a processing environment like Jupyter Notebook or any other IDE, where we can perform transformations, feature engineering, and extensive exploratory data analysis (EDA).

## 🔧 Tools & Environment
- **Language:** Python
- **Processing Engine:** Apache Spark (v3.2.2) with PySpark
- **Environment:** Local Machine using PyODBC to connect to SQL Server
- **Libraries Used:**
  - pandas, numpy, pyodbc, pyspark, databricks.koalas
  - Warnings and memory management via warnings and gc
- **Environment Notes:** Koalas is deprecated in Spark 3.2+, replaced by pyspark.pandas

## 📥 Data Ingestion
- **Source:** SQL Server database (EMP_DETAILS) table HRA_Records
- **Connection:** Established via PyODBC
- **Ingestion Strategy:**
  - Data read in chunks of 1 million rows using `pandas.read_sql_query()`
  - Concatenated into a single DataFrame and converted to Spark DataFrame with predefined schema

## 📐 Schema Definition
The dataset contains structured HR-related attributes such as:
- **Demographic:** Age, Gender, Marital Status
- **Job Role:** JobLevel, Department, JobRole, YearsAtCompany
- **Compensation:** MonthlyIncome, DailyRate, PercentSalaryHike
- **Satisfaction Metrics:** EnvironmentSatisfaction, JobSatisfaction, WorkLifeBalance
- **Attrition:** Target column indicating if an employee has left ("Yes") or stayed ("No")
- **Total Columns:** 35
- **Types:** Mostly `StringType` with some `FloatType` for numerical metrics

## 🧹 Data Cleaning Steps
- **Duplicate Removal:** Used `.dropDuplicates()` on the Spark DataFrame
- **Null/NA Check:** Planned for null count and distribution (to be expanded)
- **Casting:** Considered casting categorical numerics (like Education, JobInvolvement) to Integer for better analysis

## 🔍 Sample Insights (from first 20 rows)
- **Attrition** appears fairly distributed among departments like Sales, HR, R&D
- **MonthlyIncome** shows a wide range indicating different job levels and roles
- **OverTime** and **JobSatisfaction** may be significant factors for attrition
- Some roles are duplicated with varying features — potential for classification models

## 🗃️ Next Steps
- Generate descriptive statistics (mean, std, min, max) per numeric column
- Visualize distributions (histograms, boxplots) using pyspark.pandas or export to pandas for seaborn/matplotlib
- Explore feature correlation, especially with Attrition
- Handle imbalanced classes if model building is intended

---

# Employee Attrition EDA Summary

## 1. Distribution of Employees by Attrition
- **Insight:**  
  Employees who left the company (attrition = 1) might exhibit specific trends, such as a certain age group, department, or job role. Exploring the distribution of **Age**, **Department**, **JobRole**, and other relevant features across attrition categories can help identify if certain employee characteristics correlate with a higher likelihood of leaving.

## 2. Gender Distribution in Attrition
- **Insight:**  
  You may find that the attrition rate is higher in one gender. Analyzing the relationship between **Gender** and **Attrition** could provide insights into whether one gender tends to leave the company more than the other.

## 3. Relationship Between Job Role and Attrition
- **Insight:**  
  Employees in specific job roles (e.g., **Sales Executive**, **Laboratory Technician**) might have different attrition rates compared to other roles. A deeper exploration of **JobRole** can help uncover whether certain roles are more likely to experience higher turnover.

## 4. Correlation Between Job Satisfaction and Attrition
- **Insight:**  
  A low **JobSatisfaction** score might indicate a higher chance of attrition. Exploring the relationship between **JobSatisfaction** and **Attrition** could help identify whether dissatisfaction leads to employees leaving the company.

## 5. Impact of Work-Life Balance on Attrition
- **Insight:**  
  Employees with poor **WorkLifeBalance** might be more likely to leave. Analyzing this factor against **Attrition** can reveal whether work-life balance is a significant driver of employee turnover.

## 6. Analysis of Performance Rating vs. Attrition
- **Insight:**  
  Employees with lower performance ratings might be more likely to leave. Investigating the relationship between **PerformanceRating** and **Attrition** can help determine whether performance directly impacts attrition rates.

## 7. Distribution of Employee Age Across Attrition Categories
- **Insight:**  
  The age distribution of employees who left the company could reveal if there is any age group more likely to leave. A deeper look at the **Age** feature could also help understand whether younger or older employees are more prone to attrition.

## 8. Highest Influencing Factors on Employee Attrition
- **Insight:**  
  Factors such as **Job Satisfaction**, **Monthly Income**, **Distance From Home**, and **Work-Life Balance** might show strong correlations with attrition. An analysis of these features could provide a deeper understanding of what drives employees to leave the company.

## 9. Impact of Education Level on Attrition Rates
- **Insight:**  
  Employees with a **Master's degree** or **PhD** might have different attrition rates compared to those with **Bachelor's** or **Below College** education. Analyzing the relationship between education level and attrition could reveal if highly educated employees tend to stay longer or leave more often.

## 10. Tenure and Attrition
- **Insight:**  
  Employees with shorter tenure might have higher attrition rates, while those with longer tenure may be less likely to leave. A visualization of tenure vs. attrition could reveal trends in employee retention.

## 11. Compensation vs. Attrition
- **Insight:**  
  Employees with lower salaries or hourly rates may be more likely to leave the company. Analyzing the correlation between **Income** and **Attrition** could give insights into whether compensation is a key factor in employee turnover.

## 12. Number of Companies Worked at and Attrition
- **Insight:**  
  Employees who have worked at multiple companies might have different retention patterns compared to those with more stable career paths. A feature like **NumCompaniesWorked** could help uncover if more job-hopping correlates with a higher likelihood of attrition.

## 13. Impact of Distance From Home on Attrition
- **Insight:**  
  Employees with longer commute times might have higher attrition rates. An analysis of **DistanceFromHome** can provide insights into whether employees who live farther away from the workplace are more likely to leave.

## 14. Business Travel Frequency and Attrition
- **Insight:**  
  Employees who travel more frequently for work might have higher or lower attrition rates depending on the nature of the work and travel benefits. An analysis of **BusinessTravel** against **Attrition** can help to determine whether travel frequency affects employee retention.

## 15. Job Level vs. Attrition
- **Insight:**  
  Employees in higher job levels might have lower attrition rates, as they may have more stability, benefits, and responsibilities. Analyzing **JobLevel** and **Attrition** could uncover patterns between seniority and retention.

---

### Conclusion:
By diving into the above aspects, you can better understand the factors influencing employee attrition. These insights could help in identifying actionable steps to improve retention strategies within the organization. This analysis highlights the power of using data-driven approaches in HR management and the role of data tools like **Apache Spark** and **PyODBC** in unlocking insights from large-scale datasets.
