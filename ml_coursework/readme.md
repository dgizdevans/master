# **Predicting E-commerce Purchase Intent**

This repository contains the coursework project for the **Machine Learning and Predictive Analytics** module. The project demonstrates how clickstream data from web analytics can be transformed into predictive signals for purchase intent classification.

---

## **Project Overview**

The objective of this project is to build a binary classification model that predicts whether an e-commerce session will result in a purchase. The focus is on feature engineering and domain-driven data transformation rather than algorithm complexity.

### **Dataset**
- **Source**: Public GA4 dataset from Google Merchandise Store (`bigquery-public-data.ga4_obfuscated_sample_ecommerce`)
- **Scale**: 4.3 million events from 270,000 users over 92 days
- **Challenge**: Extreme class imbalance — only 1.35% of sessions end with a purchase (1:73 ratio)

### **Workflow**
1. **Event Taxonomy**:
   - Grouped events by funnel position: engagement, product interaction, checkout
   - Observed conversion rates: 1.14% → 4.89% → 20.26% (ratio 1:4:17)

2. **Data Cleaning**:
   - Removed 28,831 post-purchase events to prevent target leakage
   - Preserved temporal integrity for valid prediction

3. **Feature Engineering**:
   - Conversion-weighted scoring using empirical funnel ratios
   - Aggregated 3M+ events into 360K session-level records with 43 features

4. **Model Training**:
   - Compared Logistic Regression and Random Forest
   - Used stratified split (80/20) and balanced class weighting

---

## **Key Findings**

- **Near-parity between models**: ROC-AUC 0.9962 (LR) vs 0.9968 (RF), difference of 0.0006
- **Recall**: 99.28% for both models
- **Feature importance**: `checkout_score` at 28.4%, device and traffic source under 2%
- **Conclusion**: Feature engineering matters more than algorithm choice

---

## **Tech Stack**

### **Data & ML**:
- **BigQuery**: Data extraction and initial exploration
- **Python**: `pandas`, `numpy`, `scikit-learn`
- **Visualization**: `matplotlib`, `seaborn`

### **Methods**:
- Stratified train/test split
- StandardScaler for feature normalization
- RandomizedSearchCV for hyperparameter tuning
- VIF analysis for multicollinearity check

---

## **Files**

- `ml_course_Notebook.ipynb` — Full analysis pipeline: EDA, feature engineering, model training, evaluation
- `ml_course_Report.pdf` — Formal coursework report with methodology and results

---

## **Related**

📝 Medium article: [Where Web Analytics Meets Machine Learning: A Purchase Prediction Case Study](#) *(link to be added)*
