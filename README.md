# Student Depression Analysis — SQL Server & Tableau

## Project Overview

This project analyzes a dataset of **502 students** containing academic, lifestyle, financial and mental-health-related attributes.

The project uses **Microsoft SQL Server** for data preparation and exploratory analysis and **Tableau** for interactive visualization.

The goal is to understand how different student characteristics are distributed across the dataset and explore how factors such as academic pressure, study satisfaction, sleep duration, study hours, financial stress, family history of mental illness and suicidal thoughts are associated with the recorded depression outcome.

> **Important:** This is an exploratory data-analysis project. The analysis identifies patterns and associations in the dataset; it does not establish medical or causal relationships.

---

# 🎯 Problem Statement

Student well-being can be influenced by multiple academic, lifestyle and financial factors. A structured analysis of student-level data can help identify patterns in the dataset and highlight areas that may require further investigation.

This project analyzes student data to answer questions such as:

- How is depression distributed among the students?
- How are students distributed by gender and age group?
- How are academic pressure and study satisfaction distributed?
- How do sleep duration and study hours vary across students?
- How is financial stress distributed?
- How common are reported suicidal thoughts in the dataset?
- How does the recorded depression outcome vary across selected student characteristics?

---

# 🎯 Project Objectives

- Load and inspect the student dataset.
- Perform basic data-quality checks using SQL.
- Standardize inconsistent categorical values.
- Create an age-group feature.
- Convert and standardize the depression field.
- Generate frequency-based analysis for important variables.
- Connect the SQL Server dataset to Tableau.
- Build an interactive Tableau dashboard.
- Present the major patterns found in the dataset.

---

# 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft SQL Server** | Data storage, cleaning and analysis |
| **SQL** | Data transformation and aggregation |
| **Tableau** | Data visualization and dashboarding |
| **CSV** | Original dataset |
| **Tableau Workbook (.twb)** | Dashboard/report definition |

---

# 📂 Dataset

The dataset contains **502 student records** and 11 original columns.

### Main Variables

| Variable | Description |
|---|---|
| Gender | Student gender |
| Age | Student age |
| Academic Pressure | Recorded academic pressure level |
| Study Satisfaction | Recorded study satisfaction level |
| Sleep Duration | Student's reported sleep-duration category |
| Dietary Habits | Dietary-habit category |
| Suicidal Thoughts | Whether the student reported having suicidal thoughts |
| Study Hours | Reported daily study hours |
| Financial Stress | Recorded financial-stress level |
| Family History of Mental Illness | Whether a family history was reported |
| Depression | Recorded depression outcome |

---

# 🔄 Steps Followed

## Step 1: Load the Dataset

The CSV dataset was loaded into Microsoft SQL Server.

A database named:

```text
Tableau Project 1
```

was created.

The main table used in the project is:

```text
Depression_Student_Dataset
```

---

# 🔍 Step 2: Initial Data Inspection

The dataset was inspected using SQL queries such as:

```sql
SELECT *
FROM [dbo].[Depression_Student_Dataset];
```

The project also checked the distribution of categorical variables using `GROUP BY`.

For example:

```sql
SELECT Gender, COUNT(*)
FROM [dbo].[Depression_Student_Dataset]
GROUP BY Gender;
```

---

# 🧹 Step 3: Data Quality Checks

The SQL workflow checked for missing or blank gender values:

```sql
SELECT *
FROM [dbo].[Depression_Student_Dataset]
WHERE Gender IS NULL;
```

and:

```sql
SELECT *
FROM [dbo].[Depression_Student_Dataset]
WHERE Gender = ' ';
```

The structure of the table was also inspected through:

```sql
SELECT *
FROM INFORMATION_SCHEMA.COLUMNS
WHERE TABLE_NAME LIKE 'Depression_Student_Dataset';
```

---

# 🔤 Step 4: Standardizing Gender

The SQL script standardizes gender values.

For example:

```sql
UPDATE [dbo].[Depression_Student_Dataset]
SET Gender = 'M'
WHERE Gender = 'Male';
```

and:

```sql
UPDATE [dbo].[Depression_Student_Dataset]
SET Gender = 'F'
WHERE Gender = 'female';
```

This creates a more consistent representation of gender categories.

---

# 👥 Step 5: Creating Age Groups

An additional `Age_Group` column was created:

```sql
ALTER TABLE [dbo].[Depression_Student_Dataset]
ADD Age_Group varchar(max);
```

Students were grouped into three categories:

```text
A1 → 18–24
A2 → 25–30
A3 → 31+
```

using a SQL `CASE` expression:

```sql
UPDATE [dbo].[Depression_Student_Dataset]
SET Age_Group =
CASE
    WHEN Age BETWEEN 18 AND 24 THEN 'A1'
    WHEN Age BETWEEN 25 AND 30 THEN 'A2'
    ELSE 'A3'
END;
```

The resulting groups were then analyzed using:

```sql
SELECT Age_Group, COUNT(*)
FROM [dbo].[Depression_tudent_Dataset]
GROUP BY Age_Group;
```

---

# 📊 Step 6: Exploratory SQL Analysis

Frequency analysis was performed for the major variables.

### Academic Pressure

```sql
SELECT Academic_Pressure, COUNT(*)
FROM [dbo].[Depression_Student_Dataset]
GROUP BY Academic_Pressure;
```

### Study Satisfaction

```sql
SELECT Study_Satisfaction, COUNT(*)
FROM [dbo].[Depression_Student_Dataset]
GROUP BY Study_Satisfaction;
```

### Sleep Duration

```sql
SELECT Sleep_Duration, COUNT(*)
FROM [dbo].[Depression_Student_Dataset]
GROUP BY Sleep_Duration;
```

### Dietary Habits

```sql
SELECT Dietary_Habits, COUNT(*)
FROM [dbo].[Depression_Student_Dataset]
GROUP BY Dietary_Habits;
```

### Study Hours

```sql
SELECT Study_Hours, COUNT(*)
FROM [dbo].[Depression_Student_Dataset]
GROUP BY Study_Hours;
```

### Financial Stress

```sql
SELECT Financial_Stress, COUNT(*)
FROM [dbo].[Depression_Student_Dataset]
GROUP BY Financial_Stress;
```

### Family History

```sql
SELECT Family_History_of_Mental_Illness, COUNT(*)
FROM [dbo].[Depression_Student_Dataset]
GROUP BY Family_History_of_Mental_Illness;
```

---

# 🧠 Step 7: Depression Outcome Standardization

The SQL workflow also standardizes the depression field.

The column was altered to support text values:

```sql
ALTER TABLE [Depression_Student_Dataset]
ALTER COLUMN Depression varchar(Max);
```

Then the values were standardized:

```sql
UPDATE [Depression_Student_Dataset]
SET Depression = 'No'
WHERE Depression = '0';

UPDATE [Depression_Student_Dataset]
SET Depression = 'Yes'
WHERE Depression = '1';
```

The final distribution was checked using:

```sql
SELECT Depression, COUNT(*)
FROM [Depression_Student_Dataset]
GROUP BY Depression;
```

---

# 📈 Step 8: Tableau Visualization

The cleaned SQL Server table was connected to Tableau.

The Tableau workbook contains a dashboard named:

```text
Student Count Analysis
```

The workbook includes visual analyses for:

- Academic Pressure & Student Count
- Financial Stress & Student Count
- Sleep Duration & Student Count
- Study Hours & Student Count
- Study Satisfaction & Student Count

The corresponding Tableau worksheets are:

```text
AP&SC
FS&SC
SD&SC
SH&SC
SS&SC
```

---

# Dashboard Preview
<img width="1352" height="905" alt="Image" src="https://github.com/user-attachments/assets/e6c4b4f5-45f5-40a3-ba90-63edb493825d" />

---

# Key Findings

The following findings are calculated from the CSV dataset included in this repository.

## 1. Dataset Size

The dataset contains:

**502 students**

with ages ranging from:

**18 to 34 years**

The average age is approximately:

**26.24 years**

---

## 2. Depression Distribution

| Depression | Students |
|---|---:|
| Yes | 252 |
| No | 250 |

The dataset therefore contains a nearly even split between the two recorded depression categories.

---

## 3. Gender Distribution

| Gender | Students |
|---|---:|
| Male | 267 |
| Female | 235 |

The dataset contains slightly more male than female students.

---

## 4. Age Groups

| Age Group | Students |
|---|---:|
| 18–24 | 200 |
| 25–30 | 180 |
| 31+ | 122 |

The **18–24** age group contains the largest number of students in the dataset.

---

## 5. Academic Pressure

| Academic Pressure | Students |
|---|---:|
| 1 | 99 |
| 2 | 88 |
| 3 | 125 |
| 4 | 92 |
| 5 | 98 |

A rating of **3** is the most frequent academic-pressure level in the dataset.

---

## 6. Study Satisfaction

| Study Satisfaction | Students |
|---|---:|
| 1 | 86 |
| 2 | 100 |
| 3 | 103 |
| 4 | 116 |
| 5 | 97 |

A study-satisfaction rating of **4** is the most frequent category.

---

## 7. Sleep Duration

| Sleep Duration | Students |
|---|---:|
| 7–8 hours | 128 |
| More than 8 hours | 128 |
| 5–6 hours | 123 |
| Less than 5 hours | 123 |

The two largest sleep-duration categories are **7–8 hours** and **more than 8 hours**.

---

## 8. Study Hours

Study hours range from:

**0 to 12 hours**

The most frequently recorded study-hour value is:

**10 hours — 53 students**

---

## 9. Financial Stress

| Financial Stress | Students |
|---|---:|
| 1 | 110 |
| 2 | 102 |
| 3 | 100 |
| 4 | 94 |
| 5 | 96 |

A financial-stress rating of **1** is the most frequent category.

---

## 10. Suicidal Thoughts

| Reported Suicidal Thoughts | Students |
|---|---:|
| Yes | 260 |
| No | 242 |

The dataset records **260 students** as reporting suicidal thoughts.

This is a descriptive statistic from the dataset and should not be interpreted as a clinical conclusion.

---

## 11. Family History of Mental Illness

| Family History | Students |
|---|---:|
| No | 265 |
| Yes | 237 |

The dataset contains slightly more students without a recorded family history of mental illness.

---

## 12. Depression and Suicidal Thoughts

A cross-tabulation of the two variables shows:

| Suicidal Thoughts | Depression: No | Depression: Yes |
|---|---:|---:|
| No | 179 | 63 |
| Yes | 71 | 189 |

This shows a strong **association within this dataset** between the two recorded variables.

It should **not** be interpreted as proof that one variable causes the other.

---

---

# 🚀 How to Run the Project

## 1. Download the Repository

```bash
git clone <your-github-repository-url>
cd Student-Depression-Analysis
```

## 2. SQL Server

Create the database:

```sql
CREATE DATABASE [Tableau Project 1];
```

Then run the SQL script:

```text
sql/Depression student data.sql
```

Update the SQL Server connection settings if your local SQL Server configuration is different.

## 3. Tableau

Open:

```text
tableau/Student Count Analysis.twb
```

The workbook is configured to use a local SQL Server connection.

You may need to update the connection to point to your own SQL Server instance.

---

# 🔐 Security & Privacy Note

The Tableau workbook uses a local SQL Server connection.

Do not commit:

- Database passwords
- Personal credentials
- Private connection strings
- API keys
- Sensitive student information

The dataset included in this repository should be treated as a dataset for analytical/educational use.

---

# 🎯 Skills Demonstrated

- SQL
- Microsoft SQL Server
- Data Cleaning
- Data Quality Checking
- Data Transformation
- Exploratory Data Analysis
- Aggregation & Grouping
- CASE Statements
- Tableau
- Dashboard Development
- Data Visualization
- Business/Analytical Question Formulation
- Data Interpretation

---

# 💼 Project Outcome

This project demonstrates an end-to-end analytical workflow:

```text
CSV Dataset
     ↓
SQL Server
     ↓
Data Quality Checks
     ↓
Data Transformation
     ↓
Exploratory SQL Analysis
     ↓
Tableau
     ↓
Interactive Dashboard
     ↓
Insights
```

The project demonstrates how SQL and Tableau can be combined to transform raw student-level data into an analytical dashboard and communicate patterns through visualization.

---

# 👤 Author

**Harsh Negi**

 Aspiring Data Analyst

**Skills:** SQL • Microsoft SQL Server • Tableau • Python • Power BI • Excel • Data Analysis
