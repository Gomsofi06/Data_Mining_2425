# <center>Data Mining Project</center>

<center>
Master in Data Science and Advanced Analytics <br>
NOVA Information Management School
</center>

** **

<center>
Group 19 <br>
Jan-Louis Schneider, 20240506  <br>
Marta Boavida, 20240519  <br>
Matilde Miguel, 20240549  <br>
Sofia Gomes, 20240848  <br>
</center>

** **

## <center>*ABCDEats Inc*</center>

Customer segmentation project for **ABCDEats Inc.** (fictional food delivery platform).  
Built an end-to-end pipeline to **clean, engineer, transform and cluster** customer data, producing **6 interpretable segments** and an **interactive interface** for exploring cluster insights and assigning new customers to clusters.

## Key highlights
- Dataset with **52 numerical** and **4 categorical** variables (~**31,098** customers).
- Robust preprocessing: missing values, inconsistencies, and outlier handling.
- **+10 engineered features** capturing customer behavior (spending patterns, loyalty, preferences, time-based habits).
- Clustering benchmark: **Hierarchical (Ward)** vs **K-Means**; final decision favors **6 clusters** for richer segmentation.
- **Perspective-based clustering** (grouping features by viewpoint) and a final combined model.
- Interactive interface to:
  - inspect a single cluster (boxplot/heatmap/cohesion),
  - compare clusters (radar, feature-difference bars, distance plots, overlap),
  - explore all clusters (multiple plots, incl. 3D),
  - add a new customer and assign it to a cluster.

## Problem statement
Segment customers into meaningful groups to support **targeted marketing**, personalization, and better business decisions.

## Data
- **Customers:** ~31k
- **Features:** 52 numerical + 4 categorical  
- Typical issues addressed:
  - missing values (e.g., `last promo`, `customer age`, `customer region`, `first order`),
  - inconsistent rows (e.g., customers with no orders),
  - extreme outliers (e.g., unrealistic counts).

> Note: the dataset was provided in an academic context and may not be included in this repository.

## Repository contents
This repository is notebook-driven. The recommended execution order is:

1. `01_Explore_Data.ipynb` — initial exploration and data understanding  
2. `02_Processing_Data.ipynb` — cleaning (missing values, inconsistencies, outliers)  
3. `03_Feature_Engineering.ipynb` — creation of new features (+10)  
4. `04_Visualizations.ipynb` — exploratory and cluster-related plots  
5. `05_Data_transformation.ipynb` — encoding, transformations, scaling  
6. `06_Clustering.ipynb` — model training/benchmarking and final clustering  
7. `07_Interface.ipynb` — interactive interface for insights + new customer assignment  

Additional files:
- `New_Features.ipynb` — feature engineering notes/experiments
- `utils.py` — shared helper functions used across notebooks

## Methodology

### 1) Data exploration & quality checks
- Column types validation (e.g., casting certain fields to integer).
- Duplicate removal (very low duplication rate).
- Missingness analysis (including correlation of missing values).
- Distribution inspection for numerical/categorical variables.

### 2) Cleaning & imputation
- Inconsistencies fixed (e.g., logical constraints between vendor/product counts).
- Missing values:
  - Numerical: median and **KNN imputation** (for specific fields)
  - Categorical: mode
- Outliers: combined **automatic + manual** strategy to avoid removing too much data.

### 3) Feature engineering (+10 new features)
Created features to capture customer behavior and value, e.g.:
- spending aggregates,
- average spend per order/product,
- loyalty and chain preference,
- cuisine variety,
- preferred ordering day / time window.

### 4) Transformation & scaling
- Frequency encoding for some categorical variables (e.g., promo/payment).
- One-hot encoding for remaining categorical variables (not used for clustering features).
- Log transformation for numerical variables.
- Scaling:
  - Min-Max scaling to [0,1]
  - adjusted standardization for groups of features with incompatible scales.

### 5) Clustering & model selection
- **Hierarchical clustering** (Ward linkage) explored with 4–6 clusters; selected **6** for interpretability and actionable segmentation.
- **K-Means** suggested fewer clusters (best at 4), but final choice remained Hierarchical (6 clusters) for more nuanced profiles.
- Perspective-based clustering: separate clustering from different feature “views” (e.g., preferences, purchase behavior, age/time) and combined into a final segmentation.

## Final segments (6 clusters)
High-level interpretation of the final clusters:
- **Cluster 0:** Regular customers, higher spending
- **Cluster 1:** Largest group of regular customers
- **Cluster 2:** Frequent orders, low loyalty (variety-seeking)
- **Cluster 3:** High frequency, small orders
- **Cluster 4:** Best spending / most valuable customers
- **Cluster 5:** Least spending customers (needs activation)

## Interactive interface
The interface supports:
- **Insights in one cluster** (boxplot, heatmap, cohesion)
- **Compare clusters** (radar, difference bars, distances, distribution overlap)
- **Insights into all clusters** (multiple plots incl. interactive 3D)
- **Connect new entry to cluster**
  - “Quick prediction”: assigns based on centroid distance (fast)
  - “Calculate cluster”: recomputes clustering with the new point (more accurate, slower)


