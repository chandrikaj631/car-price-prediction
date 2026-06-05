CarIQ — Used Car Price Prediction

A machine learning web application that predicts used car prices based on vehicle features, with an interactive dashboard for browsing and filtering cars.
Screenshot 2026-04-12 185935.png
Screenshot 2026-04-12 185537.png

Project Overview

CarIQ is a two-page Streamlit web application powered by a tuned Random Forest Regressor trained on the CarDekho used car dataset (~15,000 records). Users can browse and filter available cars, view market insights through interactive charts, and get an instant AI-based price prediction by entering vehicle specifications.

Problem Statement

The used car market in India is highly unstructured — prices for similar cars can vary by lakhs depending on the seller, location, and negotiation. Buyers often overpay and sellers underprice due to lack of data-driven guidance.
Goal: Build a regression model that accurately estimates the fair market price of a used car based on its age, mileage, engine specs, fuel type, and other features — and deploy it as an accessible web application.

Approach

The project follows a complete end-to-end ML workflow:

Data Collection → EDA → Feature Engineering → Model Training
→ Model Comparison → Hyperparameter Tuning → Model Saving → Streamlit Deployment

Step 1 — Data Collection

Downloaded the CarDekho dataset programmatically from GitHub using urllib. Dataset contains used car listings with price, specifications, and seller information.

Step 2 — Exploratory Data Analysis (EDA)

Univariate analysis: KDE plots and box plots for all numerical features to understand distributions and detect outliers
Categorical analysis: Count plots for brand, seller type, fuel type, transmission type
Bivariate analysis: Scatter plots of each feature vs. selling price to identify linear and non-linear relationships
Correlation heatmap: Identified max_power, engine, and vehicle_age as the strongest price predictors
Chi-squared tests: Validated statistical significance of all categorical features against selling price
Business insights: Top 10 most sold cars (Hyundai i20 leads), top brands (Maruti dominates), highest-mileage brands, most expensive listings

Step 3 — Feature Engineering

Dropped high-cardinality text columns: car_name, brand, model (not useful for ML directly)
Applied one-hot encoding on: seller_type (3 categories), fuel_type (5 categories), transmission_type (2 categories)
Final feature matrix: 16 input features

Step 4 — Feature Importance

Used ExtraTreesRegressor to rank feature importance before model training. Top features: max_power, engine, km_driven, vehicle_age, mileage.

Step 5 — Model Training & Comparison

Trained 6 regression models on an 80/20 train-test split and compared performance:
ModelR² ScoreNotesLinear RegressionLowAssumes linearity — poor fit for car pricesRidge RegressionLowL2 regularization, still linearLasso RegressionLowL1 regularization, still linearSupport Vector RegressionLowStruggles with large, noisy datasetsDecision Tree RegressorModerateOverfits without pruningRandom Forest Regressor (Tuned)BestEnsemble method — handles non-linearity and outliers well

Step 6 — Hyperparameter Tuning

Applied RandomizedSearchCV on RandomForestRegressor with:

100 iterations, 3-fold cross-validation
Search space: n_estimators [100–500], max_depth [None, 10–50], min_samples_split [2,5,10], min_samples_leaf [1,2,4], max_features ['sqrt','log2'], bootstrap [True, False]
Best estimator saved as best_model.pkl

Step 7 — Deployment
Built a two-page Streamlit app with background image, custom CSS, sidebar filters, KPI cards, charts, and a prediction form.

 Tech Stack
 
LibraryVersionPurposePython3.8+Core languageStreamlitLatestWeb application frameworkScikit-learnLatestML models, RandomizedSearchCV, metricsPandasLatestData loading, filtering, manipulationNumPyLatestNumerical arrays, input encodingMatplotlibLatestStatic visualizations in notebookSeabornLatestStatistical plots — KDE, heatmap, scatterPlotlyLatestInteractive plotsSciPyLatestChi-squared statistical testsPickleBuilt-inModel serialization and loading

 Dataset
 
PropertyDetailSourceCarDekho (via GitHub)Size~15,000 recordsTargetselling_price (₹)Numerical featuresvehicle_age, km_driven, mileage, engine, max_power, seatsCategorical featuresseller_type, fuel_type, transmission_type

Application Pages

Page 1 — CarIQ Dashboard (by22.py)
The main landing page for car browsing and market exploration.
Sidebar filters:

Price Range (slider)
Location, Brand, Fuel Type, Transmission, Seats (multi-select)

Features:

🏆 Best car suggestion from filtered results (lowest price)
📊 KPI cards — Avg Price, Min Price, Max Price, Best Mileage
📋 Top 20 filtered cars table
📈 Bar charts — Cars by Brand, Fuel Type Distribution
🎯 Car selector → navigates to Price Predictor page

Page 2 — Price Predictor (appcv5.py)
AI-powered price prediction form.
Inputs: Vehicle Age, KM Driven, Mileage, Engine CC, Max Power, Seats, Seller Type, Fuel Type, Transmission
Output: Estimated price in ₹ (auto-formatted as Lakhs or Crores)

 Run Locally
 
1. Clone the repository
bashgit clone https://github.com/chandrikaj631/car-price-prediction.git
cd car-price-prediction
2. Install dependencies
bashpip install -r requirements.txt
3. Generate the trained model

 best_model.pkl is not included due to GitHub's 100MB file size limit. Run the notebook to regenerate it:

bashjupyter notebook cardekho__1_.ipynb
Run all cells — the last cell saves best_model.pkl to your working directory.
4. Launch the app
bashstreamlit run by22.py

 requirements.txt
streamlit
pandas
numpy
scikit-learn
matplotlib
seaborn
plotly
scipy
jupyter
pickle-mixin

📁 Project Structure
car-price-prediction/
├── by22.py                    # Page 1 — CarIQ Dashboard
├── pages/
│   └── appcv5.py              # Page 2 — Price Predictor
├── cardekho__1_.ipynb         # EDA + model training notebook
├── car_data.csv               # Processed dataset
├── car_bg.jpg                 # App background image
├── logo.png                   # CarIQ logo
├── requirements.txt           # Python dependencies
└── README.md

 Future Improvements

 Deploy on Streamlit Cloud (free hosting)
 Display model accuracy metrics (R², RMSE) inside the app
 Add SHAP explainability — show which features drove each prediction
 Include location-based price adjustment
 Add car image lookup by model name
 Integrate live CarDekho API for real-time listings

