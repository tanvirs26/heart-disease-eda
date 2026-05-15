# Heart Disease Dataset — Exploratory Data Analysis (EDA)

This repository holds an exploratory data analysis of the UCI Heart Disease 
dataset, sourced via `ucimlrepo`. The dataset contains clinical measurements 
from 303 patients and is commonly used for heart disease prediction research 
(https://archive.ics.uci.edu/dataset/45/heart+disease). This repository 
covers the EDA portion of a larger collaborative project. Feature engineering 
and predictive modeling were completed separately by a partner and are not 
included in this notebook.

## Overview
The dataset records clinical attributes for patients at the Cleveland Clinic, 
with a target variable indicating the presence and severity of heart disease 
on a scale of 0 to 4. This project reformulates the target as a binary 
classification problem, 0 (No Disease) vs. 1 (Disease Present, severity 
1–4 grouped together), for the purpose of EDA. Unlike predictive modeling 
projects, this work focuses exclusively on data cleaning, preprocessing, and 
visual and statistical exploration to identify which clinical features are 
most strongly associated with heart disease.

## Summary of Work Done

### Data
- Type: Clinical patient records, output: binary heart disease classification
- Size: 303 patients, 13 clinical features, 1 target variable
- Final dataset size after cleaning: 297 rows
- Mild class imbalance present between healthy and diseased patients
- Missing values found only in `ca` and `thal`

### Preprocessing / Clean Up
- Removed rows with missing values in `ca` and `thal` (small number of 
  affected entries)
- Converted multi-class target variable into binary classification using 
  a severity threshold:
  - `0` = No heart disease
  - `1` = Heart disease present (severity levels 1–4 grouped together)
- Verified categorical vs. numerical feature types across all 13 attributes
- Ensured dataset consistency before proceeding to visualization

### Data Visualization
EDA included a correlation heatmap, KDE plots, count plots, and probability 
bar charts comparing feature distributions between healthy and diseased 
patients. Key findings:

**Correlation Heatmap** — the first look at relationships between numerical 
features and the binary target. `oldpeak` showed the strongest positive 
correlation with heart disease, while `thalach` (maximum heart rate) showed 
a strong negative correlation, indicating lower heart rates are associated 
with disease presence.

<img width="768" height="511" alt="image" src="https://github.com/user-attachments/assets/3d5da48d-aafb-4a99-8456-221fc9cfb59e" />

**KDE Plots** — used to visualize the distribution of continuous features 
split by class. `oldpeak` and `thalach` showed the clearest separation 
between healthy and diseased patients.

<img width="584" height="455" alt="image" src="https://github.com/user-attachments/assets/d37020c5-7c72-4833-a1ac-109eb6b12eaa" />


<img width="576" height="455" alt="image" src="https://github.com/user-attachments/assets/b1a6c6e9-372f-4aaf-8f60-baf5c1c40609" />


**Count Plots** — plotted categorical features by class to show raw 
frequency distributions. Features like `cp` (chest pain type) and `thal` 
(thalassemia type) showed visually distinct distributions between classes.

<img width="1989" height="990" alt="image" src="https://github.com/user-attachments/assets/5d2a9e46-478a-4df0-8e42-aa984f58581d" />


**Probability Bar Charts** — quantified the relationship between each 
categorical feature and heart disease presence. These plots confirmed the 
strongest class separations:

- `ca` (number of major vessels colored) → strongest predictor; clear 
  monotonic increase in disease probability with vessel count
- `cp` (chest pain type) → highly indicative; certain pain types far more 
  associated with disease
- `thal` (blood flow defect type) → strong relationship with diagnosis
- `exang` (exercise-induced angina) → moderate predictor
- `fbs` (fasting blood sugar) → showed very little variation across 
  classes and minimal predictive value

<img width="1989" height="990" alt="image" src="https://github.com/user-attachments/assets/45a060ae-38f7-4dc0-8c1e-5fdf912e9925" />
  

### Problem Formulation
- Input: 13 raw clinical features including age, sex, chest pain type, 
  resting blood pressure, cholesterol, fasting blood sugar, resting ECG, 
  maximum heart rate, exercise-induced angina, ST depression, ST slope, 
  number of vessels, and thalassemia type
- Output: binary classification — 0 (No Disease) or 1 (Disease Present)
- Scope: This project covers EDA only. No predictive models were trained.
- Feature importance was assessed through probability based visual analysis 
  rather than model coefficients or feature importance scores

### Feature Importance (EDA-Based)
Key metric: probability difference between classes for each feature, 
assessed visually through bar charts and KDE plots.

| Feature | Importance | Notes |
|---|---|---|
| `ca` | High | Strongest class separation observed |
| `cp` | High | Highly indicative of disease presence |
| `thal` | High | Strong relationship with diagnosis |
| `exang` | Moderate | Clear but less extreme separation |
| `slope` | Moderate | Visible trend across classes |
| `restecg` | Moderate | Some differentiation between classes |
| `fbs` | Low | Minimal variation across classes |

### Conclusions
- `ca`, `cp`, and `thal` emerged as the strongest clinical indicators of 
  heart disease based on probability separation between classes
- Exercise-related features (`oldpeak`, `thalach`, `exang`) showed clear 
  physiological differences between healthy and diseased patients, 
  suggesting exercise stress reveals meaningful cardiac signals
- Fasting blood sugar (`fbs`) contributed very little discriminative 
  information and would likely be a weak predictor in any downstream model
- Even with a small dataset of ~300 patients, the data shows strong 
  structure and well-separated class distributions across several features

## How to Reproduce Results
1. Install the required packages listed below
2. Run all cells in the notebook from top to bottom
3. The `ucimlrepo` package will automatically fetch the dataset — no manual 
   download required
4. The notebook will produce all EDA visualizations in order

## Overview of Files in Repository
- README.md: project overview and analysis summary
- HeartDiseaseEDA.ipynb: full analysis including data loading, cleaning, 
  preprocessing, and all visualizations

## Software Setup
Required packages:
- numpy
- pandas
- matplotlib
- seaborn
- ucimlrepo

Install all packages with: pip install numpy pandas matplotlib seaborn ucimlrepo

## Data
The dataset is fetched automatically via the `ucimlrepo` package:

```python
from ucimlrepo import fetch_ucirepo
heart_disease = fetch_ucirepo(id=45)
```

No manual download is required. The original dataset is also available at:
https://archive.ics.uci.edu/dataset/45/heart+disease
## Citations
- Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1989). Heart Disease [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C52P4X.
