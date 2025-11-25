# Southern California Housing Market Analysis  


This project analyzes Southern California home prices using exploratory data analysis, feature engineering, and multiple predictive modeling approaches. We evaluate Linear Regression, Ridge Regression, and XGBoost to understand how different algorithms capture the complexity of the market.

---

## 📂 1. Data Loading & Initial Exploration

The dataset was imported and examined for structure, types, and summary statistics. Initial EDA focused on:

- Distributions of price, bedrooms, bathrooms, and square footage  
- City-level differences  
- Correlations among features  

Price was heavily right-skewed, and the city variable showed strong categorical variation.

---

## 📊 2. Exploratory Data Analysis (EDA)

We visualized key patterns using histograms, scatterplots, and correlation heatmaps.  
Major takeaways:

- Square footage is one of the strongest predictors of price.
- Cities vary widely in median price.
- The dataset includes expensive homes that extend well into the long tail.

---

## 🧹 3. Data Preprocessing

### 3.1 Missing Values
No missing values were present, but the preprocessing pipeline includes median imputation for future robustness.

### 3.2 Outlier Detection (IQR)
The IQR method flagged potential outliers in price, but none were removed. Keeping them preserves the integrity of real-world market variability.

---

## 🛠️ 4. Feature Engineering

We created additional features to better capture spatial and structural characteristics:

- **price_per_sqft**  
- **sqft_per_room** (with division-by-zero protection)  
- **total_rooms**  
- **bath_to_bed_ratio**  

These engineered features provide information not contained in raw counts.

---

## 🔢 5. Encoding

City names were converted to integer IDs using label encoding, enabling their use in regression models that require numerical inputs.

---

## 🤖 6. Modeling

We trained and evaluated **three** models:

### **1. Linear Regression**
- Baseline model  
- Simple, interpretable  
- R² ≈ 0.35  
- Coefficients show sqft and bathrooms as strong positive predictors  
- bath_to_bed_ratio had a large negative coefficient due to multicollinearity

### **2. Ridge Regression**
- Adds L2 regularization to penalize large coefficients  
- Helped reduce coefficient instability from multicollinearity  
- Performance was slightly improved over plain Linear Regression  
- Better generalization, lower variance in predictions

### **3. XGBoost Regressor**
- Flexible tree-based gradient boosting model  
- Captures nonlinearities and feature interactions  
- Significantly improved predictive accuracy  
- Outperformed both Linear and Ridge models on all metrics  
- Handles skewed data and heterogeneous feature importance more effectively

---

## 📈 7. Evaluation

We used an 80/20 train-test split and compared models using:

- **RMSE**
- **MAE**
- **R²**
- **Residual plots**
- **Predicted vs Actual price plots**
- **Feature importance charts (for XGBoost)**

### Model Comparison Summary
- **Linear Regression:** Reasonable baseline, interpretable but limited  
- **Ridge Regression:** Slight improvement via regularization  
- **XGBoost:** Clear winner, capturing nonlinear relationships and reducing error significantly  

Residual plots showed:

- Linear and Ridge errors grow substantially for high-priced homes  
- XGBoost maintains tighter residual spread, especially in the upper price range  

---

## 🧠 8. Conclusions

- The housing market exhibits strong nonlinearity that linear models cannot fully capture.  
- Ridge Regression improves stability but not enough to overcome structural limits.  
- XGBoost delivers the best results by modeling complex interactions and city-level effects.  
- Feature engineering helped all models but benefited XGBoost most.

---

## 🚀 9. Next Steps

Potential future improvements:

- Explore hyperparameter tuning for XGBoost  
- Incorporate more geographic features (latitude/longitude, neighborhood clustering)  
- Perform cross-validation beyond a single 80/20 split  
- Consider LightGBM or CatBoost for further nonlinear modeling  

