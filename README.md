# Wine Quality Comparative Study: Multi-Class Classification

## 🎯 Project Overview

A comprehensive machine learning comparative study to predict wine quality scores using multi-class classification. This project analyzes **red and white wine datasets** side-by-side, comparing two classification models (**Logistic Regression vs. Random Forest**) to answer key business questions about dataset difficulty, model performance, and class-level predictions.

---

## 📊 Problem Statement

Given two tabular datasets containing lab-measured chemical properties of wines, the goal was to:

1. **Red vs White Dataset**: Determine which dataset is easier to predict and why
2. **Model vs Model**: Compare model performance on each dataset
3. **Class-level Difficulty**: Identify which quality scores are hardest to predict

### Key Challenges
- **Class Imbalance**: Quality scores 3, 4, 8, 9 are significantly underrepresented
- **Overlapping Classes**: Similar quality levels (5, 6) have overlapping feature distributions
- **Multi-class Complexity**: 6-7 quality classes vs binary classification

---

## 📁 Project Structure

```
Machine_Learning/
├── README.md                                          # This file
├── Wine_Quality_Comparative_Study_PamalHarpreetSingh_PGDSAIML1.ipynb   # Main analysis (Notebook)
├── ML_Assignment_01.ipynb                             # Additional analysis
├── ML_Assignment_Multi-Class Wine Quality Classification.pdf  # Assignment brief
└── dataset/
    ├── winequality-red.csv                            # Red wine dataset (1,599 samples)
    └── winequality-white.csv                          # White wine dataset (4,898 samples)
```

---

## 📈 Dataset Description

### Features (11 total)
- **fixed acidity**: Stable acids in wine
- **volatile acidity**: Acetic acid (higher values reduce quality)
- **citric acid**: Adds freshness
- **residual sugar**: Sugar left after fermentation
- **chlorides**: Salt content
- **free sulfur dioxide**: Preservative (SO₂ levels) - Free portion
- **total sulfur dioxide**: Preservative (SO₂ levels) - Total amount
- **density**: Related to alcohol and sugar
- **pH**: Acidity level
- **sulphates**: Stability and preservation
- **alcohol**: Alcohol percentage

### Target Variable
- **quality**: Integer rating (3-9) - treated as separate classes for multi-class classification

### Dataset Statistics

| Dataset | Samples | Features | Classes | Imbalance Ratio |
|---------|---------|----------|---------|-----------------|
| Red Wine | 1,599 | 11 | 6 (3-8) | Moderate |
| White Wine | 4,898 | 11 | 7 (3-9) | High |

---

## 🔬 Methodology

### Task 1: Data Loading & Inspection
- Loaded both CSV files with proper separator (`sep=";"`)
- Verified data shape, columns, and target variable
- Confirmed 11 features in each dataset

### Task 2: Data Quality Checks
- Checked for missing values: **None found** ✓
- Checked for duplicates: **0 duplicates** ✓
- Analyzed quality class distribution (counts & percentages)
- Created bar charts to visualize class imbalance

**Key Finding**: White wine dataset is more imbalanced than red wine

### Task 3: Data Preparation
- Created feature matrix (X) and target vector (y)
- Applied stratified train-test split:
  - `test_size=0.2`
  - `random_state=42` (for reproducibility)
  - `stratify=y` (preserve class distribution)
- **Result**: Training set stratification preserved ~80:20 split across all classes

### Task 4: Baseline Model - Logistic Regression
**Pipeline**: StandardScaler → LogisticRegression(max_iter=5000)

**Red Wine Results:**
- Accuracy: 0.5906
- Macro F1-score: 0.2776
- Hardest classes: 3, 4, 8 (0.00 recall)

**White Wine Results:**
- Accuracy: 0.5490
- Macro F1-score: 0.2367
- Hardest classes: 3, 8, 9 (0.00 recall)

### Task 5: Advanced Model - Random Forest
**Model**: RandomForestClassifier(n_estimators=300, random_state=42)

**Red Wine Results:**
- Accuracy: 0.6844 ⬆️ (+15.9% improvement)
- Macro F1-score: 0.4107 ⬆️ (+47.9% improvement)
- Hardest classes: 3, 4 still challenging

**White Wine Results:**
- Accuracy: 0.6724 ⬆️ (+22.4% improvement)
- Macro F1-score: 0.4223 ⬆️ (+78.4% improvement)
- Hardest classes: 3, 9 still challenging

---

## 📋 Comparative Results Summary

| Dataset | Model | Accuracy | Macro F1-Score | Key Observation |
|---------|-------|----------|----------------|-----------------|
| Red | Logistic Regression | 0.5906 | 0.2776 | Poor recall for rare classes |
| **Red** | **Random Forest** | **0.6844** | **0.4107** | **Best accuracy; classes 3,4 remain hard** |
| White | Logistic Regression | 0.5490 | 0.2367 | Lowest overall performance |
| White | Random Forest | 0.6724 | 0.4223 | Highest F1-score; extreme classes still challenging |

---

## 🔍 Key Findings & Insights

### 1. Which Dataset Was Easier to Predict?
✅ **Red wine** dataset proved marginally easier to predict with consistently higher accuracy across both models.

**Why?**
- Red wine has moderate class imbalance (more balanced distribution)
- White wine has extreme imbalance (quality 9 = 0.10% of data)
- Red wine class separation is relatively better

### 2. Which Model Performed Better?
✅ **Random Forest** significantly outperformed Logistic Regression by 15-22% accuracy improvement across both datasets.

**Why?**
- Random Forest captures complex, non-linear relationships
- Handles the multi-dimensional feature space more effectively
- Better at dealing with correlated features
- More robust to outliers

### 3. Which Quality Classes Were Most Confusing?
❌ **Extreme classes (3, 4, 8 for red; 3, 4, 8, 9 for white)** were consistently hardest to predict.

**Why?**
- **Severe class imbalance**: Very few training samples (< 4%)
- **Limited learning**: Models can't learn meaningful patterns with sparse data
- **Feature overlap**: Extreme quality wines may have similar feature distributions to middle classes
- **Underrepresentation**: Models naturally biased toward majority classes

---

## 💡 Recommendations & Next Steps

### Immediate Improvement Attempts
1. **Class Weight Balancing** (`class_weight="balanced"`): Penalize misclassification of minority classes
2. **Convert to 3 Classes** (Low/Med/High): Merge extreme classes for better data distribution
3. **Hyperparameter Tuning**: Optimize Random Forest parameters (depth, learning rate, etc.)
4. **Feature Engineering**: Create interaction terms or polynomial features

### Proposed Next Step
🎯 **Convert to 3-class problem (Low/Med/High qualit)**: This would significantly improve predictions for currently problematic extreme classes by increasing their sample representation.

---

## 🛠️ Technologies & Libraries

- **Python 3.x**
- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computations
- **scikit-learn**: Machine learning models and metrics
  - Pipeline, StandardScaler, LogisticRegression, RandomForestClassifier
  - train_test_split, confusion_matrix, classification_report, f1_score
- **matplotlib & seaborn**: Data visualization
- **Jupyter Notebook**: Interactive analysis environment

---

## 📊 How to Use

### 1. Clone the Repository
```bash
git clone https://github.com/pamalsingh/Machine_Learning.git
cd Machine_Learning
```

### 2. Install Dependencies
```bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

### 3. Run the Analysis
```bash
jupyter notebook Wine_Quality_Comparative_Study_PamalHarpreetSingh_PGDSAIML1.ipynb
```

### 4. View Results
- All outputs, visualizations, and metrics are embedded in the notebook
- Confusion matrices and classification reports displayed for all 4 model-dataset combinations
- Comparative summary table at the end

---

## 📌 Key Deliverables

✅ **Section 1**: Problem Statement & Data Description  
✅ **Task 1**: Data loading and inspection (both datasets)  
✅ **Task 2**: Data quality checks, class distribution analysis, and comparative answers  
✅ **Task 3**: Stratified train-test split (test_size=0.2, random_state=42, stratify=y)  
✅ **Task 4**: Logistic Regression baseline with full metrics  
✅ **Task 5**: Random Forest model with full metrics  
✅ **Task 6**: Comprehensive comparison table with all confusion matrices and classification reports  
✅ **Task 7**: Final conclusions and next-step recommendations  

---

## 📚 Learning Outcomes

Through this project, I demonstrated:
- **Multi-class classification** methodology
- **Comparative model analysis** with consistent evaluation metrics
- **Class imbalance** problem identification and recognition
- **Pipeline-based** machine learning workflows
- **Stratified sampling** for fair data splits
- **Comprehensive evaluation** using accuracy, F1-score, confusion matrices, and classification reports
- **Data-driven insights** and actionable recommendations

---

## 📄 Files Description

| File | Purpose |
|------|---------|
| `Wine_Quality_Comparative_Study_PamalHarpreetSingh_PGDSAIML1.ipynb` | Main Jupyter notebook with complete analysis, code, outputs, and visualizations |
| `winequality-red.csv` | Red wine dataset (1,599 samples, 12 columns including quality) |
| `winequality-white.csv` | White wine dataset (4,898 samples, 12 columns including quality) |
| `ML_Assignment_Multi-Class Wine Quality Classification.pdf` | Original assignment brief with detailed requirements |
| `README.md` | This comprehensive project documentation |

---

## 📧 Contact & Attribution

**Project**: Wine Quality Comparative Study  
**Author**: Pamal Harpreet Singh  
**Batch**: PGDSAIML1  
**Date**: April 2026

---

## 📜 License

This project is for educational purposes. Dataset sourced from wine quality UCI Machine Learning Repository.

---

## 🔗 Repository

**GitHub**: [https://github.com/pamalsingh/Machine_Learning](https://github.com/pamalsingh/Machine_Learning)

For the complete analysis with all outputs and visualizations, visit the repository and open the Jupyter Notebook file.
