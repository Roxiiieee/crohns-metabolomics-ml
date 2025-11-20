# Comparative Analysis of Biological Samples for Crohn’s Disease Diagnosis Using Machine Learning 

This repository contains the full implementation of my machine-learning project evaluating four biological sample types: **blood, breath, faeces, and urine**, for their diagnostic utility in **Crohn’s Disease (CD)**.  

Metabolomic data was collected via **GC-MS** (.MAT files), parsed into structured DataFrames, visualised as chromatograms, and analysed using **Support Vector Machines (SVM)** and **Random Forest** classifiers. The notebook performs full classification, bootstrap validation, permutation testing, and visualisation for all sample types.

---

## 📄 Project Overview

This project investigates which biological matrix provides the most reliable metabolomic signature for distinguishing Crohn’s Disease from healthy controls. GC-MS chromatograms were analysed from 4 sample types:
- **Blood**
- **Breath**
- **Faeces**
- **Urine**

Two datasets were used for each sample type:  
- **CD_All** (CD vs all other conditions)  
- **CD_Ctrl** (CD vs healthy controls)

Full details, figures, tables, and analysis appear in the accompanying report.

---

## 🧬 Methods

### **1. Data Parsing**
GC-MS `.MAT` files were parsed using a custom function:
- Extracts XTIC (ion counts)  
- Retrieves sample names  
- Extracts retention times  
- Loads class labels (1 = CD, 2 = control)  
- Produces a clean DataFrame:  
  - Rows = samples  
  - Columns = retention times  
  - `Label` column appended  

### **2. Exploratory Analysis**
Chromatograms were generated for CD vs Control samples to visually inspect metabolic differences.

### **3. Machine Learning Models**

#### **Support Vector Machine (SVM)**
- Baseline SVC (default hyperparameters)
- Evaluated on both datasets
- Confusion matrices visualised

#### **Random Forest**
- Baseline 100-tree ensemble
- Evaluated similarly
- Often reached 100% accuracy on raw data  
  → **further examined via bootstrap & permutation to check for overfitting**

### **4. Model Validation**

#### **Bootstrap Validation**
- 100 iterations  
- Random 70/30 train/test split each time  
- Accuracy distribution plotted

#### **Permutation Testing**
- Class labels permuted  
- Tests whether accuracy > chance  
- Overlapping histograms visualised  

---

## 🧪 Results Summary

Faecal samples performed best overall, with both SVM and RF showing the clearest discriminative power, especially in the CD_Ctrl dataset.

Key findings (all backed by figures in the report):
- **Faeces > Urine > Blood > Breath** (in terms of diagnostic usefulness)
- Blood and breath showed overlapping chromatograms → weaker signals
- Faecal samples contained diverse metabolic signatures reflective of gut inflammation  
- Random Forest frequently overfit (100% accuracy) but bootstrap/permutation exposed the real generalisable performance (~0.70–0.85 depending on sample type)

Full results table is automatically generated at the end of the notebook.  

---

## 📊 Technologies Used

- Python 3.8 or higher  
- NumPy  
- Pandas  
- SciPy (for `.mat` parsing)  
- Matplotlib  
- Scikit-Learn (SVM, RandomForest, train/test splitting)

---

## 📦 Requirements

There is no `requirements.txt` included because the entire project ran inside Jupyter.  
The notebook uses the following packages:
- numpy
- pandas
- matplotlib
- scipy
- scikit-learn

---

## 🚫 Dataset Availability

The GC-MS `.mat` files **cannot be included** due to data privacy and ethical restrictions.  

## 📌 Notes

- The project is implemented entirely in **one Jupyter Notebook**, as submitted.  
- Bootstrap and permutation curves may take several minutes to run if recomputed.  
