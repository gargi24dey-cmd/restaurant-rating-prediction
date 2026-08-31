# Predicting Restaurant Rating Categories

## Random Forest vs Logistic Regression: A Comparative Analysis of Zomato and Swiggy

This project uses machine learning classification techniques to predict restaurant rating categories and compare model performance across two food-delivery platforms: **Zomato and Swiggy**.

The analysis focuses on Bangalore restaurants and uses **Orange Data Mining** to build reproducible machine learning workflows. Two classification algorithms — **Random Forest** and **Logistic Regression** — are compared to determine which performs better for predicting restaurant rating categories.

---

## Project Objectives

The project aims to:

* Predict whether a restaurant belongs to a **Low, Medium, or High** rating category.
* Compare the performance of **Random Forest** and **Logistic Regression**.
* Identify how restaurant characteristics such as **cost, votes, services, and restaurant type** differ across rating categories.
* Compare rating patterns and model performance between **Zomato and Swiggy**.

---

## Dataset

### Zomato Bangalore Restaurants

**Source:** Kaggle — Zomato Bangalore Restaurants Dataset

* Raw records: **51,717**
* Records after cleaning: **41,418**
* Retention: approximately **80%**
* Rating categories:

  * Low: `< 3.5`
  * Medium: `3.5–4.0`
  * High: `> 4.0`

### Features Used

* `online_order`
* `book_table`
* `votes`
* `rest_type`
* `listed_in(type)`
* `cost_clean`
* `Platform`

Meta information such as restaurant name and cuisines was also retained.

### Swiggy Bangalore Restaurants

**Source:** Kaggle — Swiggy Bangalore Restaurants Dataset

* Raw records: **10,298**
* Records after cleaning: **1,499**
* Retention: approximately **14.6%**
* Features:

  * `Area`
  * `Category`
  * `cost_clean`

The Swiggy dataset contained a large number of missing ratings. Additionally, no restaurant in the cleaned sample had a rating above 4.0, resulting in a predominantly **Low/Medium** classification problem.

---

## Data Cleaning

The raw restaurant datasets required preprocessing before modelling.

The main cleaning steps included:

1. Parsing rating values such as `"4.1/5"`.
2. Removing commas and converting restaurant cost into numeric values.
3. Handling unusable rating values such as `"NEW"` and `"–"`.
4. Removing observations without usable numeric ratings.
5. Creating the `rating_class` target variable.
6. Encoding categorical variables before model training.

The preprocessing was performed within the **Python Script widget in Orange Data Mining**, keeping the workflow reproducible within Orange.

---

## Machine Learning Models

### 1. Logistic Regression

Logistic Regression was used as a linear and interpretable baseline model.

It assumes that the predictors contribute to the outcome through additive relationships. This makes it relatively easy to interpret but limits its ability to capture complex interactions between variables.

### 2. Random Forest

Random Forest is an ensemble learning algorithm based on multiple decision trees.

It was selected because restaurant characteristics may interact in non-linear ways. For example, the effect of restaurant cost may differ depending on the restaurant's popularity and number of votes.

---

## Orange Data Mining Workflow

The main Zomato workflow consists of:

```text
Dataset
   ↓
Python Script
   ↓
Select Columns
   ↓
Preprocess
   ↓
 ┌─────────────────────┐
 ↓                     ↓
Logistic Regression   Random Forest
 └──────────┬──────────┘
            ↓
       Test & Score
            ↓
     Confusion Matrix
```

A similar workflow was constructed for the Swiggy dataset.

Model evaluation used **5-fold stratified cross-validation**.

---

## Key Findings

### Zomato

Random Forest substantially outperformed Logistic Regression on the Zomato dataset.

| Model               |       AUC |
| ------------------- | --------: |
| Random Forest       | **0.928** |
| Logistic Regression | **0.778** |

Random Forest achieved a **19.4 percentage-point accuracy advantage** over Logistic Regression in the reported comparison.

The results suggest that restaurant rating patterns involve non-linear relationships and interactions that are better captured by tree-based models.

---

### Swiggy

The Swiggy dataset produced a very different outcome.

| Model               |       AUC |
| ------------------- | --------: |
| Random Forest       | **0.537** |
| Logistic Regression | **0.600** |

Both models performed only slightly better than random classification.

The main reason is the structure of the available Swiggy data: only **1,499 restaurants** had usable ratings, and approximately **82% belonged to the Medium category**.

Therefore, the model has considerably less information with which to distinguish rating categories.

---

## Business Insights

### Cost and Restaurant Ratings

The analysis found a strong association between restaurant cost and rating category.

A one-way ANOVA produced:

**F = 4708.6, p < 0.001**

Higher-rated restaurants generally had higher associated costs, although this represents an **association rather than causation**.

### Votes and Restaurant Ratings

Restaurant votes, used as a proxy for customer engagement and popularity, also differed significantly across rating categories.

The ANOVA produced:

**F = 5866.1, p < 0.001**

Higher-rated restaurants tended to have substantially greater customer engagement.

### Platform Differences

The comparison demonstrates that model performance depends not only on the algorithm but also on the structure and quality of the underlying platform data.

Zomato provided considerably more variation in rating categories, while the Swiggy sample was heavily concentrated around Medium ratings.

---

## Tools & Technologies

* **Python**
* **Orange Data Mining**
* **Machine Learning**
* **Random Forest**
* **Logistic Regression**
* **5-Fold Cross-Validation**
* **ANOVA**
* **Data Visualization**
* **Kaggle datasets**

---

## Project Structure:

```text
restaurant-rating-prediction/
│
├── README.md
│
├── data/
│   ├── zomato.csv - The original dataset is approximately 500 MB and therefore is not included in the GitHub repository due to GitHub's file-size limitations.
                     https://www.kaggle.com/datasets/himanshupoddar/zomato-bangalore-restaurants
│   └── swiggy.csv - Included in this repository for reproducibility.
│
├── orange/
│   ├── restaurant rating prediction.ows
│   
│
├── report/
│   └── Restaurant_Rating_Prediction_Report.pdf
│
└── images/
    ├── zomato_distribution.png
    ├── cost_boxplot.png
    ├── votes_boxplot.png
    └── roc_comparison.png
```

---

## Future Scope

Potential extensions of the project include:

* Investigating interactions between **cuisine type and cost**.
* Incorporating **delivery time** and **order volume** where available.
* Testing a finer **five-level rating classification** instead of three categories.
* Including platform-specific variables to better explain Swiggy ratings.
* Exploring additional machine learning algorithms for comparison.

---

## References

1. Zomato Bangalore Restaurants Dataset — Kaggle.
2. Swiggy Bangalore Restaurants Dataset — Kaggle.
3. Orange Data Mining — University of Ljubljana, Bioinformatics Laboratory.

---

## Author

**Gargi Dey**

MSc Economics (Data Analytics)

Symbiosis School of Economics
