# Used Car Price Driver Analysis (CRISP-DM)

An end-to-end machine learning project utilizing the **CRISP-DM (Cross-Industry Standard Process for Data Mining)** framework to identify, analyze, and rank the core factors influencing used vehicle valuation. This analysis provides actionable, data-driven inventory recommendations for automotive dealerships.

---

## 📊 Executive Summary & Inventory Recommendations

Based on our statistical modeling of over 400,000 used vehicle listings, we have identified the primary features that dictate market price. Dealership management should immediately pivot inventory acquisition strategy to align with the following high-value consumer drivers:

### 1. Core Drivers of Premium Prices (What to Buy)
* **Prioritize "New" Vehicles:** Vehicles listed in **"new"** or **"like new"** condition command a massive premium (adding over 10,000 USD and 3,500 USD to baseline value respectively). 
* **Transmission Types:** Interestingly, standard manual transmissions hold a slight positive premium relative to standard automatic configurations in this specific market cut, while specialized transmission types ("other") see highly elevated values.

### 2. Core Drivers of Price Depreciation (What to Avoid)
* **Fuel Type is Highly Sensitive:** Standard **Gas** and **Hybrid** vehicles show the sharpest drop-off in baseline value relative to the market baseline. 
* **Drive Configuration:** Front-Wheel Drive (**fwd**) cars are priced significantly lower than All-Wheel Drive or Rear-Wheel Drive setups. Avoid over-indexing inventory on standard front-wheel-drive city commuters if maximum vehicle margin is desired.
* **Salvage & Fair Condition:** Vehicles labeled as **"salvage"** drop by roughly 7,500 USD. Avoid purchasing vehicles requiring heavy reconditioning, as the market penalty far outweighs the initial acquisition discount.

### 3. Next Steps & Continuous Monitoring
While car **Year** and **Odometer** mileage show the expected predictable baseline impacts, the real vehicle value is driven by condition metrics and drivetrain configurations. We recommend implementing an automated screening tool based on these model rules to flag underpriced "like-new" vehicles at regional auctions for immediate purchase.

---

## 🛠️ Technical Methodology

### 1. Data Understanding & Preparation
* **Dataset:** Evaluated an initial footprint of 426,880 rows and 18 features.
* **Outlier Mitigation:** Extracted and eliminated extreme noise, restricting the pricing scope exclusively to the realistic consumer market range of 500 USD to 100,000 USD.
* **Feature Engineering:** Permanently dropped non-predictive operational variables (`id`, `VIN`, and `size`).
* **Imputation:** Resolved missing categorical data by enforcing an `'unknown'` structural baseline, and stabilized missing numerical data points by applying feature-specific medians.
* **Encoding:** Applied full One-Hot Encoding (`pd.get_dummies`) across all categorical parameters to convert text-based inputs into unified numeric representations for model consumption.

### 2. Modeling & Evaluation
To maintain algorithmic rigor, the clean dataset was divided into an **80/20 train/test split**. We implemented and evaluated two distinct variations of supervised regression:

* **Model 1: Ordinary Least Squares (OLS) Linear Regression**
  * Baseline $R^2$ Score: `0.3760`
* **Model 2: Ridge Regression with Hyperparameter Tuning**
  * Conducted a robust grid search optimization over multiple regularization strengths (`alpha`).
  * Utilized **5-Fold Cross-Validation** to guarantee model stability and mitigate data leakage.
  * Tuned $R^2$ Score: `0.3760` (Alpha: 1)

---

## 📁 Repository Structure
* `prompt_II.ipynb` - The primary Jupyter Notebook documenting all Python code, data visualizations, and execution cells.
* `README.md` - Executive report and methodology summary.

> *Note: The source data file (`vehicles.csv`) contains over 426k rows and has been omitted from this repository due to GitHub's file size storage boundaries. The notebook is structured using a relative data path (`data/vehicles.csv`) to seamlessly process local files.*
