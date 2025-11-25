# Housing Price Prediction with Linear Regression

This project analyzes home prices using a Linear Regression model. It covers data preprocessing, feature engineering, encoding, modeling, and performance evaluation using a dataset of 15,474 entries - SoCal Real Estate specifically

---

## 📌 1. Data Preprocessing

### **Imputation**
The dataset did not contain missing values, but the pipeline includes median imputation for any numerical feature that may contain missing entries in future datasets.

### **Outlier Analysis (IQR)**
The IQR method was used to detect potential price outliers. No entries were removed to preserve full market variation.  
Some negative lower bounds appeared due to the IQR formula—these do not indicate real negative home values, only that no low-end outliers exist.

---

## 📌 2. Feature Engineering

Four new features were added:

- **price_per_sqft**: `price / sqft`
- **sqft_per_room**: `sqft / bedrooms` (bedrooms of 0 were replaced with 1 to avoid division by zero)
- **total_rooms**: `bedrooms + bathrooms`
- **bath_to_bed_ratio**: `bathrooms / bedrooms`

These features capture spatial efficiency and structural density beyond raw room counts.

---

## 📌 3. Encoding

City names were converted to integer IDs because linear regression requires numerical input. Each unique city string was mapped to a unique integer.

---

## 📌 4. Modeling Pipeline

### **Selected Features**
- `bed`
- `bath`
- `sqft`
- `city_encoded`
- `sqft_per_room`
- `total_rooms`
- `bath_to_bed_ratio`

The target variable is **price**.

### **Train/Test Split**
- **80% training:** 12,379 samples  
- **20% testing:** 3,095 samples  

A Linear Regression model was trained on the processed training set.

---

## 📌 5. Coefficient Interpretation

Key coefficients:

- **Intercept:** $244,842.70
- **bath:** +104,797.24  
- **bed:** –74,488.77  
- **bath_to_bed_ratio:** –265,859.88  
- **sqft & total_rooms:** positive contributions with smaller magnitudes  

The negative ratio coefficient results from multicollinearity. When controlling for individual bed/bath features, the ratio can indicate fewer bedrooms rather than more bathrooms.

---

## 📌 6. Model Performance

### **Predicted vs Actual**
Scatter plots show wide dispersion around the ideal line, explaining the moderate R² value.

### **Residual Behavior**
- Residuals cluster near zero for low-priced predictions.
- Error increases substantially for high-priced predictions.
- Patterns are consistent across train/test splits.

### **Residual Distributions**
Both sets show roughly normal, zero-centered distributions—an indication of unbiased errors.

### **Metrics**
| Metric | Value | Interpretation |
|--------|--------|----------------|
| **RMSE** | $309,313.21 | Avg. error ~43.7% of mean home price |
| **MAE** | $228,128.65 | Typical absolute error |
| **R²** | 0.3509 | Explains ~35% of price variance |

These results reflect the limits of a purely linear model on a nonlinear market.

---

## 📌 7. Deeper Model Analysis

- Square footage is the strongest positive predictor.
- City encoding captures major regional pricing differences.
- Multicollinearity complicates interpretation of bed/bath ratio features.
- Large residuals and moderate R² show that nonlinear relationships dominate the dataset.

Linear regression remains a useful baseline but cannot capture complex interactions in housing markets.

---

## 📌 8. Next Steps

Future improvements include:

- **Ridge / Lasso Regression**: reduce multicollinearity and stabilize coefficients.
- **Tree-based models**: Random Forests, Gradient Boosted Trees for nonlinear relationships.
- **Location-based enrichment**: neighborhood or zipcode features.

---

## 📁 Project Structure
