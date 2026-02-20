
<p align="center">
  <img src="https://img.icons8.com/ios-filled/200/1e40af/health-insurance.png" width="100" alt="Health Insurance Cost Predictor" />
</p>

<h2 align="center">Health Insurance Cost Predictor</h2>
<p align="center"><b>A Streamlit-powered app to estimate individual health insurance premiums in real time.</b></p>

<p align="center">
  <a href="https://streamlit.io/"><img alt="Streamlit" src="https://img.shields.io/badge/Streamlit-1.45.0-ff4b4b?logo=streamlit&logoColor=white"></a>
  <a href="https://numpy.org/"><img alt="NumPy" src="https://img.shields.io/badge/NumPy-2.2.5-013243?logo=numpy&logoColor=white"></a>
  <a href="https://pandas.pydata.org/"><img alt="Pandas" src="https://img.shields.io/badge/Pandas-2.2.3-150458?logo=pandas&logoColor=white"></a>
  <a href="https://scikit-learn.org/"><img alt="scikit-learn" src="https://img.shields.io/badge/scikit learn-1.6.1-F7931E?logo=scikit-learn&logoColor=white"></a>
  <a href="https://xgboost.readthedocs.io/"><img alt="XGBoost" src="https://img.shields.io/badge/XGBoost-3.0.2-1A733A?logo=xgboost&logoColor=white"></a>
  <a href="https://joblib.readthedocs.io/"><img alt="Joblib" src="https://img.shields.io/badge/Joblib-1.5.0-3776AB?logo=python&logoColor=white"></a>
</p>

---

## Overview

The **Health Insurance Cost Predictor** is a Streamlit application that leverages pre-trained regression models to estimate individual health insurance premiums based on user inputs such as age, BMI, smoking status, number of dependents, region, and more. By segmenting users into “young” and “rest” categories with separate models and scalers, the app delivers more accurate predictions for both demographics.

---

## Key Features

- **Interactive UI**: Clean, user-friendly sliders, dropdowns, and buttons to enter demographic, lifestyle, and medical attributes.
- **Two-Model Approach**:  
  - **Young Model**: Linear Regressor trained specifically on younger applicants.  
  - **Rest Model**: XGBoost Regressor optimized for the general adult population.
- **On-the-Fly Prediction**: Input parameters are passed through corresponding scalers and models to instantly return a cost estimate.
- **Persisted Artifacts**: Both models and their associated `Scaler` objects are serialized via Joblib and loaded at runtime.
- **Lightweight & Fast**: Built with Streamlit for rapid prototyping and deployment, no database required.

---

## Project Structure

```
Health_Insurance_Cost_Predictor/
│
├── artifacts/                      # Serialized models and scalers
│   ├── model_rest.joblib           # XGBoost model for the general adult population
│   ├── model_young.joblib          # Linear Regression model for younger users
│   ├── scaler_rest.joblib          # StandardScaler fitted on “rest” training data
│   └── scaler_young.joblib         # StandardScaler fitted on “young” training data
│
├── .gitignore                      # Git ignore rules
├── LICENSE                         # Apache License file
├── README.md                       # This documentation
├── main.py                         # Streamlit app entry point
├── prediction_helper.py            # Prediction logic: loading artifacts & processing inputs
└── requirements.txt                # Frozen Python dependencies
```

---

## Application Screenshot
https://health-insurance-premium-predictor-new.streamlit.app/

<p align="center">
  <img src="screenshot.png" alt="Health Insurance Cost Predictor UI" width="700"/>
</p>

---

## Getting Started

### Prerequisites

- Python 3.8+ installed on your system  
- `pip` (Python package installer)  
- (Optional) A virtual environment tool such as `venv` or `conda`
### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/tiknaavenger/Health_Insurance_Cost_Predictor.git
   cd Health_Insurance_Cost_Predictor
   ```

2. **Create and activate a virtual environment (recommended)**

   ```bash
   python -m venv venv
   # Windows:
   venv\Scripts\activate
   # macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

---

## Running the App

From the project root directory, simply run:

```bash
streamlit run main.py
```

Once Streamlit finishes loading, it will automatically open a browser window (or show a local URL) where you can interact with the **Health Insurance Cost Predictor**. If it doesn’t open automatically, navigate to:

```
http://localhost:8501
```

---

## How It Works

1. **User Inputs**  
   - **Age** (years)  
   - **Number of Dependents**  
   - **Income in Lakhs**  
   - **Genetical Risk** (0 = none, 1 = low, 2 = moderate, 3 = high)  
   - **Insurance Plan** (e.g., Bronze, Silver, Gold)  
   - **Employment Status** (e.g., Salaried, Self-Employed, Unemployed)  
   - **Gender** (Male/Female)  
   - **Marital Status** (Married/Unmarried)  
   - **BMI Category** (Underweight, Normal, Overweight, Obese)  
   - **Smoking Status** (No Smoking / Smoker)  
   - **Region** (Northeast, Northwest, Southeast, Southwest)  
   - **Medical History** (No Disease / Has Disease)  

2. **Segmentation**  
   - If **Age < 30**, the app loads **`scaler_young.joblib`** and **`model_young.joblib`** (Linear Regression).  
   - Otherwise, it loads **`scaler_rest.joblib`** and **`model_rest.joblib`** (XGBoost Regressor).  

3. **Scaling & Prediction**  
   - Input features are preprocessed (one-hot encoding for categorical variables, standardized numeric features via `Scaler`).  
   - The appropriate model generates a predicted premium.  

4. **Display Result**  
   - The predicted cost is displayed under the “Predict” button in a green info box.

---

## requirements.txt

```text
streamlit==1.45.0
numpy==1.26.4
pandas==2.2.3
scikit-learn==1.4.2
xgboost==2.0.3
joblib==1.3.2
```

> If you add or upgrade any packages, remember to run `pip freeze > requirements.txt` to update this file.

---

## Contributing

Contributions, issues, and feature requests are welcome! If you’d like to:

1. Fork the repository  
2. Create a new branch (`git checkout -b feature/<your-feature>` )  
3. Commit your changes (`git commit -m "Add <feature>"`)  
4. Push to the branch (`git push origin feature/<your-feature>`)  
5. Open a Pull Request  

Please ensure your code follows PEP 8 style and includes any necessary unit or integration tests.

---

## License

This project is licensed under the **Apache License 2.0**. See the [LICENSE](./LICENSE) file for details.

---

*Empower yourself with data-driven insights—predict your health insurance premium in seconds!*  
