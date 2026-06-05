# 🚗 CarIQ — Used Car Price Prediction

A machine learning web application that predicts used car prices based on vehicle features, with an interactive dashboard for browsing, filtering, and analyzing cars.

## 📸 Screenshots

### Dashboard

![Dashboard](images/dashboard.png)

### Price Predictor

![Price Predictor](images/predictor.png)

---

# 📌 Project Overview

CarIQ is a two-page Streamlit web application powered by a tuned Random Forest Regressor trained on the CarDekho used car dataset (~15,000 records).

Users can:

* Browse and filter available cars
* Explore market insights through interactive charts
* View key business metrics
* Receive instant AI-powered price predictions

The project demonstrates a complete end-to-end machine learning workflow from data collection to deployment.

---

# 🎯 Problem Statement

The used car market in India is highly unstructured. Prices for similar vehicles can vary significantly depending on factors such as seller type, location, mileage, and vehicle condition.

As a result:

* Buyers may overpay
* Sellers may underprice vehicles
* Price estimation becomes subjective

### Goal

Build a regression model capable of accurately estimating the fair market value of a used car using vehicle specifications and deploy it through an easy-to-use web application.

---

# 🔄 Approach

The project follows a complete machine learning lifecycle:

**Data Collection → EDA → Feature Engineering → Model Training → Model Comparison → Hyperparameter Tuning → Model Saving → Streamlit Deployment**

---

# 📊 Step 1 — Data Collection

* Downloaded the CarDekho dataset programmatically using Python.
* Dataset contains approximately 15,000 used car listings.

### Key Attributes

* Selling Price
* Vehicle Age
* KM Driven
* Mileage
* Engine
* Max Power
* Fuel Type
* Transmission Type
* Seller Type
* Seats

---

# 🔍 Step 2 — Exploratory Data Analysis (EDA)

### Univariate Analysis

* KDE plots
* Box plots
* Distribution analysis
* Outlier detection

### Categorical Analysis

* Brand distribution
* Seller type analysis
* Fuel type distribution
* Transmission type distribution

### Bivariate Analysis

* Feature vs Selling Price relationships
* Scatter plots
* Trend identification

### Correlation Analysis

Strongest predictors identified:

* Max Power
* Engine
* Vehicle Age

### Business Insights

* Top-selling car models
* Most popular brands
* Highest mileage brands
* Most expensive listings

---

# ⚙️ Step 3 — Feature Engineering

### Removed Features

* car_name
* brand
* model

### One-Hot Encoding Applied

* seller_type
* fuel_type
* transmission_type

### Final Dataset

* 16 input features

---

# 🌟 Step 4 — Feature Importance

Used ExtraTreesRegressor to identify influential features.

### Top Features

1. Max Power
2. Engine
3. KM Driven
4. Vehicle Age
5. Mileage

---

# 🤖 Step 5 — Model Training & Comparison

| Model                     | Performance | Notes                             |
| ------------------------- | ----------- | --------------------------------- |
| Linear Regression         | Low         | Assumes linear relationship       |
| Ridge Regression          | Low         | L2 regularization                 |
| Lasso Regression          | Low         | L1 regularization                 |
| Support Vector Regression | Low         | Struggles with large datasets     |
| Decision Tree Regressor   | Moderate    | Overfitting tendency              |
| Random Forest Regressor   | Best        | Handles non-linearity effectively |

### Selected Model

✅ Tuned Random Forest Regressor

---

# 🎯 Step 6 — Hyperparameter Tuning

Applied RandomizedSearchCV with:

* 100 iterations
* 3-fold cross-validation

### Tuned Parameters

* n_estimators
* max_depth
* min_samples_split
* min_samples_leaf
* max_features
* bootstrap

### Output

```text
best_model.pkl
```

---

# 🚀 Step 7 — Deployment

Developed a two-page Streamlit application with:

* Custom CSS
* Background image
* Interactive filters
* KPI cards
* Dynamic charts
* AI-based price prediction

---

# 🛠️ Tech Stack

| Technology   | Purpose             |
| ------------ | ------------------- |
| Python       | Core Programming    |
| Streamlit    | Web Application     |
| Pandas       | Data Manipulation   |
| NumPy        | Numerical Computing |
| Scikit-learn | Machine Learning    |
| Matplotlib   | Visualizations      |
| Seaborn      | Statistical Plots   |
| Plotly       | Interactive Charts  |
| SciPy        | Statistical Testing |
| Pickle       | Model Serialization |

---

# 📂 Dataset

| Property             | Detail                                                    |
| -------------------- | --------------------------------------------------------- |
| Source               | CarDekho Dataset                                          |
| Size                 | ~15,000 Records                                           |
| Target Variable      | selling_price                                             |
| Numerical Features   | vehicle_age, km_driven, mileage, engine, max_power, seats |
| Categorical Features | seller_type, fuel_type, transmission_type                 |

---

# 📱 Application Pages

## Page 1 — CarIQ Dashboard

### Features

* Price Range Filter
* Brand Filter
* Fuel Type Filter
* Transmission Filter
* Seat Filter
* Best Car Recommendation
* KPI Cards
* Interactive Charts
* Top 20 Cars Table

### Visualizations

* Cars by Brand
* Fuel Type Distribution
* Price Analysis

---

## Page 2 — Price Predictor

### Inputs

* Vehicle Age
* KM Driven
* Mileage
* Engine
* Max Power
* Seats
* Seller Type
* Fuel Type
* Transmission Type

### Output

* Estimated Used Car Price
* Auto-formatted in Lakhs or Crores

---

# ▶️ Run Locally

## Clone Repository

```bash
git clone https://github.com/chandrikaj631/car-price-prediction.git
cd car-price-prediction
```

## Install Dependencies

```bash
pip install -r requirements.txt
```

## Generate Model

Run:

```bash
jupyter notebook cardekho__1_.ipynb
```

Execute all cells to generate:

```text
best_model.pkl
```

## Launch Application

```bash
streamlit run by22.py
```

---

# 📁 Project Structure

```text
car-price-prediction/

├── by22.py
├── pages/
│   └── appcv5.py
├── cardekho__1_.ipynb
├── car_data.csv
├── car_bg.jpg
├── logo.png
├── requirements.txt
└── README.md
```

---

# 🔮 Future Improvements

* Streamlit Cloud Deployment
* SHAP Explainability
* Model Performance Dashboard
* Location-Based Pricing
* Car Image Lookup
* Real-Time CarDekho Integration

---


