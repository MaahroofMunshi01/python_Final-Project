# 🚢 Titanic Survival Analysis

## 📌 Project Overview

This project performs **Exploratory Data Analysis (EDA)** on the Titanic dataset to understand the different factors that influenced passenger survival.

The project explores passenger survival based on factors such as:

* Passenger Class
* Gender
* Age
* Age Groups
* Embarkation Port
* Fare
* Number of Siblings/Spouses
* Number of Parents/Children

Various charts and a correlation heatmap are used to understand the relationships within the dataset.

---

## 🎯 Project Objectives

The main objectives of this project are:

* Load and explore the Titanic dataset.
* Understand the structure and basic statistics of the data.
* Identify and handle missing values.
* Check for duplicate records.
* Analyze overall passenger survival.
* Compare survival rates across different passenger classes.
* Analyze survival rates by gender.
* Divide passengers into different age groups and compare survival rates.
* Analyze survival based on embarkation port.
* Study age distribution for survived and non-survived passengers.
* Analyze correlations between numerical variables.

---

## 📂 Dataset

The project uses the **Titanic Dataset**, which contains information about passengers aboard the Titanic.

### Dataset Information

* **Total Rows:** 891
* **Total Columns:** 12

### Important Columns

| Column        | Description                            |
| ------------- | -------------------------------------- |
| `PassengerId` | Unique passenger identification number |
| `Survived`    | Survival status (0 = No, 1 = Yes)      |
| `Pclass`      | Passenger class (1, 2, 3)              |
| `Name`        | Passenger name                         |
| `Sex`         | Passenger gender                       |
| `Age`         | Passenger age                          |
| `SibSp`       | Number of siblings/spouses aboard      |
| `Parch`       | Number of parents/children aboard      |
| `Ticket`      | Ticket number                          |
| `Fare`        | Passenger fare                         |
| `Cabin`       | Cabin information                      |
| `Embarked`    | Port of embarkation                    |

---

## 🛠️ Technologies & Libraries

The following Python libraries were used:

* **Python**
* **Pandas** – Data manipulation and analysis
* **Matplotlib** – Data visualization
* **Seaborn** – Statistical data visualization
* **Jupyter Notebook** – Development environment

### Import Libraries

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

---

## 🔍 Project Workflow

### 1. Import Libraries

The required Python libraries are imported for data manipulation and visualization.

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

### 2. Load Dataset

The Titanic CSV file is loaded using Pandas.

```python
df = pd.read_csv("titanic.csv")
```

### 3. Explore the Dataset

The project uses different Pandas functions to understand the dataset:

```python
df.shape
df.head()
df.tail()
df.describe()
```

These functions help understand the size, structure, first and last records, and statistical information of the dataset.

---

## 🧹 Data Cleaning

### Handling Missing Values

Missing values were checked using:

```python
df.isnull().sum()
```

The missing values were handled as follows:

```python
df["Age"] = df["Age"].fillna(df["Age"].median())

df["Embarked"] = df["Embarked"].fillna(
    df["Embarked"].mode()[0]
)

df["Cabin"] = df["Cabin"].fillna("Unknown")
```

### Why these methods?

* **Age:** Missing ages were filled using the median.
* **Embarked:** Since it is a categorical column, the mode was used.
* **Cabin:** Missing cabin values were replaced with `"Unknown"`.

### Checking Duplicate Records

Duplicate records were checked using:

```python
df.duplicated().sum()
```

---

# 📊 Data Analysis & Visualizations

## 1. Overall Survival Count

A count plot was created to compare passengers who survived and passengers who did not survive.

```python
sns.countplot(
    data=df,
    x="Survived",
    hue="Survived"
)
```

Where:

* `0` = Did not survive
* `1` = Survived

The survival counts were also displayed using:

```python
df["Survived"].value_counts()
```

---

## 2. Survival Rate by Passenger Class

A bar plot was used to compare survival rates among different passenger classes.

```python
sns.barplot(
    data=df,
    x="Pclass",
    y="Survived",
    errorbar=None
)
```

This visualization helps examine how survival rates varied across:

* 1st Class
* 2nd Class
* 3rd Class

---

## 3. Survival Rate by Gender

The project compares survival rates between male and female passengers.

```python
sns.barplot(
    data=df,
    x="Sex",
    y="Survived",
    errorbar=None
)
```

This helps identify differences in survival rates between the two gender categories in the dataset.

---

## 4. Survival Rate by Age Group

Passengers were divided into different age groups using `pd.cut()`.

```python
df["Age_Group"] = pd.cut(
    df["Age"],
    bins=[0, 12, 18, 35, 60, 100],
    labels=[
        "Child",
        "Teenager",
        "Young_Adult",
        "Adult",
        "Senior"
    ]
)
```

### Age Groups

| Age Range | Group       |
| --------- | ----------- |
| 0–12      | Child       |
| 12–18     | Teenager    |
| 18–35     | Young Adult |
| 35–60     | Adult       |
| 60–100    | Senior      |

A bar plot was then used to compare survival rates among these age groups.

---

## 5. Survival Rate by Gender & Passenger Class

The project also combines **gender and passenger class** to analyze survival rates.

```python
sns.barplot(
    data=df,
    x="Pclass",
    y="Survived",
    hue="Sex",
    errorbar=None
)
```

Here, `hue="Sex"` uses different colors to represent the gender categories within each passenger class.

---

## 6. Survival Rate by Embarkation Port

The Titanic passengers embarked from different ports.

The project analyzes survival rates based on the `Embarked` column.

```python
sns.barplot(
    data=df,
    x="Embarked",
    y="Survived",
    errorbar=None
)
```

The embarkation categories are:

* `S` – Southampton
* `C` – Cherbourg
* `Q` – Queenstown

---

## 7. Age Distribution by Survival

A histogram was created to visualize the distribution of passenger ages according to survival status.

```python
sns.histplot(
    data=df,
    x="Age",
    hue="Survived",
    bins=30,
    kde=True
)
```

### Parameters Used

* `bins=30` divides the age range into 30 intervals.
* `hue="Survived"` separates the distribution according to survival status.
* `kde=True` adds a smooth curve showing the overall distribution.

---

## 8. Correlation Heatmap

A correlation heatmap was created to examine relationships between selected numerical variables.

```python
numeric_data = df[
    [
        "Survived",
        "Pclass",
        "Age",
        "SibSp",
        "Parch",
        "Fare"
    ]
]

sns.heatmap(
    numeric_data.corr(),
    annot=True,
    cmap="Blues",
    fmt=".2f"
)
```

### Why these columns?

The selected columns are suitable for numerical correlation analysis.

`PassengerId` was not included because it is an identifier rather than a meaningful measurement.

Categorical columns such as `Sex` and `Embarked` were also not included in this basic correlation calculation.

### Heatmap Parameters

| Parameter      | Purpose                                      |
| -------------- | -------------------------------------------- |
| `annot=True`   | Displays correlation values inside the cells |
| `cmap="Blues"` | Sets the heatmap color scheme                |
| `fmt=".2f"`    | Displays values with 2 decimal places        |

---

# 📈 Key Analysis Areas

The project examines survival patterns across:

```text
Passenger Class
      ↓
Gender
      ↓
Age
      ↓
Age Groups
      ↓
Embarkation Port
      ↓
Gender + Passenger Class
      ↓
Numerical Correlations
```

The visualizations make it easier to compare these different factors and understand patterns within the Titanic dataset.

---

# 📁 Project Structure

```text
Titanic-Survival-Analysis/
│
├── Final_project.ipynb
├── titanic.csv
└── README.md
```

---

# ▶️ How to Run the Project

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

### 2. Open the project folder

```bash
cd Titanic-Survival-Analysis
```

### 3. Install required libraries

```bash
pip install pandas matplotlib seaborn jupyter
```

### 4. Open Jupyter Notebook

```bash
jupyter notebook
```

### 5. Open

```text
Final_project.ipynb
```

Make sure the `titanic.csv` file is available in the same folder as the notebook.

---

# 🎓 What I Learned

Through this project, I practiced:

* Loading CSV files using Pandas
* Exploring datasets
* Understanding DataFrame structure
* Handling missing values
* Checking duplicate records
* Using `groupby()`
* Creating age groups using `pd.cut()`
* Creating count plots
* Creating bar plots
* Creating histograms
* Using `hue` for categorical comparison
* Using KDE curves
* Creating correlation heatmaps
* Understanding correlation values
* Using Matplotlib and Seaborn for data visualization
* Performing basic Exploratory Data Analysis (EDA)

---

# 🚀 Future Improvements

The project can be extended by adding:

* More detailed statistical analysis
* Additional visualizations
* Feature engineering
* Interactive dashboards
* Machine learning models for survival prediction
* Model evaluation using accuracy, precision, recall, and F1-score

---

# 👨‍💻 Project Author

**Maahroof Munshi**

BCA Graduate | MCA Student
Aspiring Data Analyst 

---

⭐ **If you find this project useful, feel free to explore the notebook and give the repository a star!**
