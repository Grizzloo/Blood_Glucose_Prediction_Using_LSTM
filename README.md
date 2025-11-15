# Blood Glucose Prediction Using LSTM (Shanghai T1DM & T2DM Datasets)

This repository contains the implementation of a predictive pipeline for **blood glucose forecasting** using **Long Short-Term Memory (LSTM)** neural networks.  
The project was developed for the university course in *Biometrics* and is based on the research work:

**“Comprehensive Data Processing and Predictive Modeling of Blood Glucose Levels Using Shanghai T1DM and Shanghai T2DM Datasets”**  
*Gabriele Vittorio Coralluzzo – Mariarosaria Rossi*

---

## 🔍 Project Overview

The goal of this project is to process real-world clinical data from Type 1 and Type 2 diabetes patients and train a deep learning model capable of predicting short-term glucose variations.

The pipeline includes:

- Data extraction and cleaning (Excel/CSV files)
- Feature engineering (insulin flags, meal detection, carbohydrate estimation)
- Temporal sequence generation for LSTM models
- Deep learning training and evaluation
- Visualization of clinical and predictive results

## 📊 Datasets

### **Shanghai T1DM Dataset**
- 12 Type 1 diabetes patients  
- Continuous Glucose Monitoring (CGM)  
- Insulin doses, carbohydrate intake, timestamps  
- 3–14 days per patient  

### **Shanghai T2DM Dataset**
- Larger clinical dataset  
- CGM, antidiabetic drugs, HbA1c, lipid profile  
- Lifestyle indicators  
- Demographics and medical history  

---

## 🧹 Data Preprocessing

### ✔ Meal extraction  
`Estrazione.py` extracts the **Dietary intake** column from all patient files and aggregates it into a single Excel file.

### ✔ Carbohydrate estimation  
`Ricerca.py` uses `dieta.xlsx` to map food items to their carbohydrate content and updates each patient file.

### Additional preprocessing:
- Cleaning missing or invalid data  
- Standardizing timestamps  
- Creating insulin and meal binary flags  
- Building sliding window sequences (30–60 minutes)

---

## 🧬 Feature Set

Features used as input for the LSTM model:

- **CGM** (target series)  
- **Age**  
- **Gender** (Female=1, Male=2)  
- **BMI**  
- **Insulin-Flag** (binary)  
- **DietaryFlag** (binary)  
- **Carbs (g)**  

---

## 🤖 Model Description (LSTM)

Implemented using TensorFlow/Keras.

**Architecture**
- LSTM layer  
- Dropout layer  
- Dense output layer  
- Loss: Mean Squared Error (MSE)  
- Optimizer: Adam  

**Training**
- One model per patient  
- Sliding windows of 30 or 60 time steps  
- Target: next glucose measurement  

---

## 📈 Results

### **30-Minute Forecast**
- **R²:** 46.86%  
- **Accuracy@10%:** 51.79%  
- **MSE:** 600.40  

### **60-Minute Forecast**
- **R²:** 21.45%  
- **Accuracy@10%:** 47.83%  
- **MSE:** 838.50  

Short-term predictions are significantly more stable and accurate.

---

## 🛠 How to Run

### 1. Install dependencies
```bash
pip install pandas numpy tensorflow scikit-learn matplotlib seaborn openpyxl
````

### 2. Run preprocessing

```bash
python Estrazione.py
python Ricerca.py
```

### 3. Train the model

Open the notebooks:

* `Normalizzazione.ipynb`
* `LSTM.ipynb`

### 4. Generate clinical graphs

```bash
python boxplot.py
python boxplot1.py
```

---

## 👥 Authors

**Gabriele Vittorio Coralluzzo**
Methodology, Software, Testing, Writing
LinkedIn: [https://www.linkedin.com/in/gabriele-vittorio-coralluzzo-891248228/](https://www.linkedin.com/in/gabriele-vittorio-coralluzzo-891248228/)

**Mariarosaria Rossi**
Methodology, Software, Testing, Writing

---

## 📄 Paper

Full research paper: **ProgettoFVAB.pdf**

---

## 📜 License

This project is for academic purposes.
