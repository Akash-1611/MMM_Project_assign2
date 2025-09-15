# Marketing Mix Modeling with Mediation Assumption

## 1. Project Overview
This project applies **Marketing Mix Modeling (MMM)** to estimate the impact of different marketing and business levers (e.g., Facebook, TikTok, Snapchat, Google spend, Email/SMS, Price, Promotions) on **Revenue**.  

We also handle the **mediation assumption**:  
👉 Social media (Facebook, TikTok, Snapchat) stimulates search intent → drives **Google spend** → influences **Revenue**.  

The goal is not just prediction, but **insight**:  
- Which levers drive revenue?  
- How much do price and promotions matter?  
- How do mediated effects (Google spend) change our understanding?  

---

## 2. Dataset
- **Weekly data (2 years)** with features:
  - Paid Media (Facebook, TikTok, Snapchat, Google)
  - Direct levers (Email/SMS)
  - Business drivers (Price, Promotions, Followers)
  - Target variable: **Revenue**

---

## 3. Workflow
### Step 1: Data Preparation
- Converted week to proper datetime format.  
- Extracted year, month, week number.  
- Handled missing values with backfill/zero-fill.  
- Created **lag features** (revenue_lag1, revenue_lag2).  
- Created **rolling features** (4-week moving average & volatility).  
- Scaled inputs for consistency.

### Step 2: Modeling Approach
- Used **Random Forest Regressor** for flexibility and interpretability.  
- Performed **Hyperparameter tuning** with `RandomizedSearchCV`.  
- Used **Time Series Cross-Validation (blocked splits)** to avoid data leakage.  

### Step 3: Causal Framing
- Modeled **Google as a mediator**:  
  - Stage 1: Predict Google spend from social platforms.  
  - Stage 2: Use predicted Google spend (not actual) when modeling revenue.  
- Built a **causal DAG (graph)** to visualize assumptions.  

### Step 4: Model Evaluation
- Metrics: RMSE (error) and R² (fit).  
- Residual analysis (check for patterns).  
- Time-series CV scores.  

### Step 5: Insights & Diagnostics
- **Feature Importance** (top drivers of revenue).  
- **Sensitivity Analysis** (how changes in Price or Promotions affect revenue).  
- **Explainability with SHAP** (visualizing marginal impact of each variable).  

---

## 4. Key Results
- **Optimized Random Forest** gave robust out-of-sample performance.  
- **Google spend is strongly influenced by social channels**, confirming the mediation assumption.  
- **Price and promotions show significant elasticity** (higher promotions → higher revenue; higher price → lower revenue).  
- **Email/SMS has a consistent positive effect** but smaller than paid media.  

---

## 5. Deliverables
- Clean, reproducible code in Python (Jupyter Notebook or script).  
- Visualizations (Actual vs Predicted, Feature Importance, SHAP plots, Sensitivity curves, DAG diagram).  
- Documentation (this README).  

---

## 6. Environment Setup
To reproduce:
```bash
# Install dependencies
pip install -r requirements.txt
