Machine learning solutions for Allianz Benelux SA: customer segmentation using K-Means and PCA; predictive modeling with supervised learning, feature engineering, data preprocessing, model evaluation.

# Allianz Insurance Analytics: Customer Segmentation & Predictive Modeling

Welcome to the Allianz Insurance Analytics repository—a showcase of advanced machine learning applications in the insurance industry. Developed as a case study for Allianz Benelux SA, this project demonstrates the power of data science in transforming insurance operations.

---

## Table of Contents

- [Dataset Description](#dataset-description)
- [Project Overview](#project-overview)
- [Model 1: Customer Segmentation (Clustering)](#model-1-customer-segmentation-clustering)
- [Model 2: Predictive Modeling (Supervised Learning)](#model-2-predictive-modeling-supervised-learning)
- [How to Use](#how-to-use)
- [License](#license)
- [Intended Audience](#intended-audience)
- [Contact](#contact)

---

## Dataset Description

The analysis uses the `AllianzDisabilityClaimDataset` from the `Improving_P&L_machineLearning.xlsx` Excel file.  
Each row represents an insurance policyholder or claim, with features including:

- **Demographic information:** `Sex`, `Birth_year`, `Birth_month`, `End_age`
- **Claim details:** `Claim_year`, `Claim_month`, `Duration`, `Annuity`
- **District and location codes:** `District`, `Postalcode`, `Broker`
- **Derived features:** A set of `Pct_dis1` to `Pct_dis21` columns capturing various percentage-based or categorical risk indicators

Prior to modeling, only the `Contract_number` and `Postalcode` columns are dropped in the predictive modeling workflow.

---

## Project Overview

Allianz Benelux SA faced significant P&L losses as long-duration disability insurance claims began exceeding collected premiums. To address this, we analyzed 5,370 historical claims linked to 4,760 policies, identifying key risk factors such as age, gender, district, and broker. We built a Random Forest model to predict claim durations and applied K-Means clustering with PCA to segment customers into risk tiers. These insights enabled Allianz to implement risk-based premium strategies that reduce financial exposure and improve pricing fairness.

## Model 1: Customer Segmentation (Clustering)

### Objective

Segment insurance customers into distinct groups based on risk and claim characteristics, enabling tailored business strategies and optimized resource allocation.

### Techniques Used

- Data loading and initial exploration
- Data preprocessing (including removal of missing values)
- Feature scaling using StandardScaler
- Dimensionality reduction with PCA (to 2 components)
- Clustering using K-Means
- Cluster evaluation using silhouette score
- Cluster profiling and visualization

### Detailed Workflow

1. **Data Loading and Exploration:**  
   - Loaded the insurance claims data from the Excel sheet (`AllianzDisabilityClaimDataset`).
   - Inspected data for shape, data types, and missing values.

2. **Data Preprocessing:**  
   - Checked and removed rows with missing values to ensure data integrity for clustering.

3. **Feature Scaling:**  
   - Standardized the numeric features using `StandardScaler` to ensure all variables contribute equally to clustering.

4. **Dimensionality Reduction:**  
   - Applied Principal Component Analysis (PCA) to reduce dimensionality to 2 principal components for visualization.

5. **Clustering:**  
   - Applied KMeans clustering to the PCA-transformed data, assigning each data point to a cluster.

6. **Cluster Evaluation:**  
   - Evaluated clustering performance using the silhouette score.

7. **Cluster Profiling and Visualization:**  
   - Created summary tables and visualizations (scatter plots, boxplots, and bar charts) to interpret cluster characteristics and business relevance.

### Key Results & Visualizations

#### 1. Customer Segmentation Visualization
![Customer Segmentation (PCA + KMeans Clustering)](images/Clusters_Visualizations.png)

*Scatter plot of customer clusters in PCA-reduced space, showing distinct groups for targeted action.*

#### 2. Cluster Profile Summary Table
![Cluster Profiles Table](images/Clusters_Summary.png)

*Table comparing segment size, mean claim duration, annuity, and payout—essential for business strategy.*

#### 3. Claim Duration by Cluster
![Claim Duration Distribution by Cluster](images/Claim_Duration_By_Cluster_Colored.png)

*Boxplot analysis of claim durations across segments, revealing risk differences.*

#### 4. Annuity vs. Duration by Cluster
![Annuity vs. Duration by Cluster](images/Annuity_vs_Duration_by_Cluster_with_Centroids.png)

*Scatter plot mapping annuity against claim duration, colored by cluster with centroids highlighted.*

#### 5. Cluster Risk Profile: Mean Duration and Annuity
![Cluster Risk Profile](images/Cluster_Risk_Profile_Dual_Axis_OneLegend.png)

*Bar chart for average claim duration and annuity by segment.*

#### 6. Mean Payout per Claim by Cluster
![Mean Payout per Claim by Cluster](images/Cluster_Mean_Payout_per_Claim_Dynamic.png)

*Mean payout per claim by cluster, highlighting which segments drive costs.*

---

## Model 2: Predictive Modeling (Supervised Learning)

### Objective

Predict disability duration at the individual level, empowering Allianz to proactively identify and manage high-risk claims.

### Techniques Used

- Data loading from Excel
- Dropping unnecessary columns (`Contract_number`, `Postalcode`)
- Data visualization (distribution plots, boxplots)
- Feature scaling with StandardScaler
- Train-test split (80/20)
- Model training with RandomForestClassifier
- Model evaluation (R2, RMSE, MAE, MSE, classification report, confusion matrix)
- Deployment of an interactive prediction widget

### Detailed Workflow

1. **Data Loading and Preparation:**  
   - Loaded the data from the `AllianzDisabilityClaimDataset` sheet in the Excel file.
   - **Dropped the columns**: `Contract_number` and `Postalcode` as they were not required for modeling.
   - Checked for and handled missing values as necessary.

2. **Exploratory Data Analysis (EDA):**  
   - Visualized distributions (e.g., duration) and relationships (e.g., duration by sex, by district) using histograms and boxplots.

3. **Feature Scaling:**  
   - Standardized numeric features using `StandardScaler` to prepare data for modeling.

4. **Train-Test Split:**  
   - Split data into features (X) and target variable (`Duration` or risk flag, as used in the code).
   - Performed an 80/20 split for model validation.

5. **Model Training:**  
   - Trained a `RandomForestClassifier` on the training data.

6. **Model Evaluation:**  
   - Predicted on the test set and evaluated the model using R2 score, RMSE, MAE, MSE, and also with a classification report and confusion matrix.

#### **Evaluation Results**
- **R² Score on Test Set:** 0.9997
- **Root Mean Squared Error (RMSE):** 0.1104
- **Mean Absolute Error (MAE):** 0.0410 years
- **Mean Squared Error (MSE):** 0.0122 (years²)
  
#### 1. Actual Durations VS Perdicted Duration

![Duration VS Denisty](images/Duration_VS_Denisty.png)

*Table comparing actual duration vs perdicted duration *
#### 2. Duration VS Density

![Perdicted VS Actual](images/Perdicted_VS_Actual.png)

*Table comparing actual duration vs perdicted duration *

7. **Deployment with Widget:**  
   - Developed an interactive widget using `ipywidgets` to allow users to input feature values and receive model predictions on claim risk.

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

The Apache License 2.0 is a permissive license that allows you to:
- Use the software for any purpose
- Modify the software
- Distribute the software
- Sublicense the software
- Grant a patent license

For more details about the terms and conditions, please refer to the [LICENSE](LICENSE) file.

Last updated: 2025-05-25 12:03:17 UTC

---

## How to Use

1. **Clone the repository and install dependencies:**
   ```bash
   git clone https://github.com/yourusername/allianz-insurance-analytics.git
   cd allianz-insurance-analytics
   pip install pandas numpy scikit-learn matplotlib seaborn
