# SUPPORT2 In-Hospital Mortality Prediction

## Project Overview

This project uses the **SUPPORT2 (Study to Understand Prognoses and Preferences for Outcomes and Risks of Treatments)** dataset from the UCI Machine Learning Repository to explore the prediction of in-hospital mortality among seriously ill hospitalized patients.

The project is structured as a supervised binary classification problem. The analysis examines demographic, disease-related, physiologic, laboratory, and other clinical characteristics that may be useful for predicting whether a patient experiences in-hospital mortality.

The project includes dataset exploration, data quality assessment, preprocessing planning, exploratory data analysis, and development of a reproducible machine learning workflow.

## Research Question

**Can demographic and clinical characteristics be used to predict in-hospital mortality among seriously ill hospitalized patients in the SUPPORT2 dataset?**

The intended prediction point will be defined before model development so that predictors are restricted to information that would realistically be available when the prediction is made. This is particularly important for avoiding data leakage from variables generated later during hospitalization.

## Dataset

**Dataset:** SUPPORT2  
**Source:** UCI Machine Learning Repository  
**UCI Dataset ID:** 880

The dataset contains:

- 9,105 patient observations
- 42 predictor variables
- Demographic, socioeconomic, diagnostic, physiologic, laboratory, functional, and hospitalization-related information
- A binary in-hospital mortality outcome

The dataset can be accessed through the UCI Machine Learning Repository:

https://archive.ics.uci.edu/dataset/880/support2

The notebook retrieves the dataset programmatically using the `ucimlrepo` Python package.

## Target Variable

The primary target variable is `hospdead`, representing in-hospital mortality:

- `0` = Patient survived hospitalization
- `1` = Patient died during hospitalization

The outcome distribution is:

- Survived hospitalization: 6,745 patients (74.1%)
- In-hospital mortality: 2,360 patients (25.9%)

Because the outcome is moderately imbalanced, model performance will not be evaluated using accuracy alone.

## Exploratory Analysis

Initial exploratory analysis includes:

- Examination of dataset dimensions and variable types
- Evaluation of the binary target distribution
- Descriptive statistics for numerical predictors
- Frequency distributions for categorical predictors
- Assessment of missing data
- Investigation of potentially unusual clinical observations
- Visualization of mortality across clinically relevant patient characteristics

Initial visualizations examine:

1. Distribution of in-hospital mortality
2. In-hospital mortality rate by disease class
3. APACHE III physiology score by in-hospital mortality outcome

## Missing Data and Preprocessing

Missing data represent an important challenge in the SUPPORT2 dataset. Several predictors contain substantial missingness, including `adlp`, `urine`, `glucose`, and `bun`.

The planned preprocessing strategy will consider both the amount and potential meaning of missingness rather than automatically applying a single method to all predictors.

Potential approaches include:

- Median imputation for numerical predictors with relatively limited missingness
- Explicit missing or unknown categories for appropriate categorical variables
- Multivariable imputation using observed patient characteristics when appropriate
- Missingness indicators when the absence of a measurement may itself contain useful information
- Evaluation of whether predictors with very high missingness should be retained
- One-hot encoding of categorical predictors
- Standardization of continuous predictors for models that are sensitive to predictor scale
- Evaluation of transformations for highly skewed continuous variables

All learned preprocessing steps will be fit using training data only and incorporated into the modeling workflow to reduce the risk of data leakage.

### Connection to Graduate Capstone Research

The missing-data strategy in this project is also informed by my graduate capstone research. My capstone examines how different missing-data preprocessing strategies affect logistic regression models for ICU mortality prediction using MIMIC-IV data.

The capstone compares approaches including complete-case analysis, median imputation, median imputation with missingness indicators, and multiple imputation, with model performance evaluated using measures of discrimination and calibration.

This project provides an opportunity to apply related missing-data concepts to a different clinical population while considering how preprocessing decisions may influence mortality prediction.

## Model Evaluation

The primary candidate evaluation metric is **ROC-AUC**, which will be used to assess the model's ability to discriminate between patients who survive hospitalization and those who experience in-hospital mortality.

Additional evaluation measures may include:

- Precision-recall AUC (PR-AUC)
- Sensitivity (recall)
- Specificity
- Precision
- Brier score
- Calibration plots

Including both discrimination and calibration measures will provide a more complete assessment of model performance than accuracy alone.

## Reproducibility

The project is designed to support reproducible execution in Google Colab.

Key reproducibility practices include:

- Programmatic retrieval of the SUPPORT2 dataset from UCI
- Explicit package imports and dependencies
- Clearly organized notebook sections
- Separation of data loading, exploration, preprocessing, modeling, and evaluation
- Use of reproducible random seeds where applicable
- Training/test separation before learned preprocessing transformations
- Machine learning pipelines for preprocessing and model development
- Documentation of major analytical decisions

Before submission, the notebook will be tested using a clean runtime and executed from beginning to end to verify that cells do not depend on an unintended execution order.

## Running the Notebook

1. Open the project notebook in Google Colab or another compatible Jupyter environment.
2. Run the notebook from the first cell to install and import required packages.
3. The SUPPORT2 dataset will be retrieved programmatically from the UCI Machine Learning Repository.
4. Execute the remaining cells sequentially to reproduce the analysis.

A local copy of the SUPPORT2 dataset is not required when the UCI repository is accessible.

## Project Status

This repository currently contains the **dataset selection and final project planning stage** of the project. Model development, evaluation, interpretation, and additional reproducibility enhancements will be completed during subsequent stages of the final project.
