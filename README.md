# 4SCA
A Four-Step Comprehensive Analysis to Discover Prognostic Biomarkers and Their Roles in Personalized Skin Cutaneous Melanoma

Authors: Ananda Sutradhar, Masrur Sobhan, Bikhyat Adhikari, and Ananda Mohan Mondal




<img width="932" height="356" alt="4SCA_1_A" src="https://github.com/user-attachments/assets/f60e3522-9999-4005-8bee-81e13ab1fe99" />


## Setup

This notebook **(Complete_4SCA.ipynb)** was developed and tested in **Google Colab** using: **Python 3.12.13**


To run the notebook locally, create a Python environment with version **3.12.13** and install the required packages from **requirements.txt**.


## Running the Experiment:
Download the sample processed datasets from the dataset folder. Start the experiment with: sample_dataset.csv. 

For the final step, Prognostic Verification and Clinical Translation, survival information is required. Use the sample survival dataset:
Sample_BEST_Subset_from_Step3_with_Survival_Data.csv.csv

Note that: These are sample datasets provided for demonstration purposes. The original gene expression and survival datasets can be obtained from the UCSC Xena Browser: https://xenabrowser.net/datapages/?cohort=TCGA%20Melanoma%20(SKCM)&removeHub=https%3A%2F%2Fxena.treehouse.gi.ucsc.edu%3A443

**Workflow:**
The notebook divided into four major steps.
1. Preliminary gene screening
2. Pareto optimal gene refinement
3. Interpretable diagnostic biomarker discovery
4. Prognostic verification and clinical translation

## Step 1 — Preliminary Gene Screening:
In this step, the notebook reads the main gene expression dataset (sample_dataset.csv). The goal of this step is to perform initial gene screening and identify informative gene sets for classification.

Two feature selection techniques are applied:
ANOVA F-test
Mutual Information

For each feature selection technique, the notebook evaluates different numbers of selected genes, ranging from 300 to 10,000 genes. The selected gene sets are evaluated using the following machine learning models:

- AdaBoost
- Decision Tree
- Extra Trees
- Gradient Boosting
- K-Nearest Neighbors
- Logistic Regression
- Naive Bayes
- Random Forest
- Support Vector Classifier
- Multilayer Perceptron
- XGBoost

The purpose of this step is to identify the best-performing feature selection method, gene set size, and classification model combination.

## Step 2 — Pareto Optimal Gene Refinement:
In this step, the best feature set obtained from Step 1 is used for further optimization. Here, applies NSGA-II, a multi-objective evolutionary optimization algorithm, to identify Pareto-optimal gene subsets.

The optimization process is based on two objectives:
1. Minimize the number of selected genes
2. Maximize classification accuracy

The optimized gene subsets are evaluated using 5-fold stratified cross-validation. This step helps reduce the number of genes while maintaining strong classification performance.

## Step 3 — Interpretable Diagnostic Biomarker Discovery:
This step uses the optimized gene subset from Step 2 ('BEST_Subset_from_Step2.csv') The notebook applies SHAP analysis to interpret model predictions and identify the most influential genes.

The top three performing models from Step 2 are considered in this stage. SHAP values are calculated for these models, and genes are ranked according to their contribution to the model predictions. The goal of this step is to identify interpretable diagnostic biomarker candidates from the optimized gene set.

## Step 4 —  Prognostic Verification and Clinical Translation:
IIn this step, the selected diagnostic genes are further validated using survival analysis.

Along with the diagnostic biomarkers selected from Step 3, this stage requires survival information, including:
- Overall survival status: OS
- Overall survival time: OS.time

A sample dataset also uploaded named 'Sample_BEST_Subset_from_Step3_with_Survival_Data.csv'.
This step performs the following analyses:
- Cox proportional hazards regression
- Hazard ratio calculation
- Forest plot generation
- Kaplan-Meier survival analysis
- Log-rank test
- Risk gene visualization
- Protective gene visualization
