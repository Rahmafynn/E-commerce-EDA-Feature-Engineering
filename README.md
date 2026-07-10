
## Advanced EDA & Feature Engineering 🚀

### Project Overview
An end-to-end enterprise-grade data science 
pipeline applied to a 1,200-row e-commerce 
dataset as part of the DecodeLabs 
Industrial Training Program (Batch 2026).

### Business Problem
Transform raw, chaotic e-commerce transaction 
data into a mathematically clean dataset 
ready for machine learning algorithms.

### Dataset
- Rows      : 1,200
- Columns   : 14
- Domain    : E-commerce Orders
- Target    : TotalPrice

### Pipeline Architecture (IPO Framework)

#### Phase 1 — Input: Securing Fidelity
- Missing Value Treatment
  → CouponCode NaN treated as NO_COUPON
  → Business logic over statistical imputation
- Outlier Detection
  → IQR vs Z-Score comparison
  → IQR chosen (robust for skewed data)
- Outlier Treatment
  → Winsorization via numpy.clip()
  → Upper bound capped at 3330.40
  → Zero row loss!

#### Phase 2 — Process: Vectorized Engine
- One-Hot Encoding (drop_first=True)
  → Eliminated dummy variable trap
  → 14 columns expanded to 30
- Feature Engineering (3 new features)
  → Price_Per_Cart_Item (r=0.696 with target)
  → otherItemsInCart    (r=0.017 with target)
  → Month & DayOfWeek  (temporal features)
- Multicollinearity Check
  → Pearson correlation matrix
  → Collinearity Eradication Algorithm
  → All features independently validated

#### Phase 3 — Output: Contracts & Scaling
- Pandera Schema Validation
  → Runtime data contracts enforced
  → All 1,200 rows passed validation
- Feast Feature Store
  → Centralized feature repository
  → Eliminates training-serving skew
  → Features served consistently

### Key Statistical Decisions
- IQR over Z-Score
  (more robust for right-skewed distributions)
- Winsorization over Deletion
  (preserves row count and data integrity)
- Business Logic over KNN
  (NaN in CouponCode = no coupon used)
- drop_first=True in One-Hot Encoding
  (eliminates perfect multicollinearity)

### Engineered Features
| Feature | Formula | Correlation |
|---------|---------|-------------|
| Price_Per_Cart_Item | TotalPrice/ItemsInCart | 0.696 |
| otherItemsInCart | ItemsInCart - Quantity | 0.017 |
| Month | Extracted from Date | 0.027 |
| DayOfWeek | Extracted from Date | 0.007 |

### Tools & Libraries
- Python 3.13
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Pandera
- Feast

### Author
Rahma 
