# Food Delivery Data — Cleaning & Dashboard EDA

An end-to-end EDA project on a deliberately messy, simulated food delivery dataset (600+ orders). Combines heavy data cleaning with a multi-angle "dashboard-style" visual analysis covering restaurant performance, delivery times, order value, ratings, and trends.

## Objective
To clean a realistically messy food delivery dataset and answer a set of business-relevant questions: which restaurants perform best, how delivery time varies by city, how order status breaks down, and whether delivery speed relates to customer ratings.

## Tools Used
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn

## Data Quality Issues Identified & Fixed

| Column | Issues Found | Fix Applied |
|---|---|---|
| `restaurant_name` | Same restaurant listed under different casing/whitespace (e.g. `Spice Garden` / `SPICE GARDEN` / `spice garden`) | Standardized casing, stripped whitespace — reduced 17 raw values to 11 true restaurants |
| `cuisine_type`, `city`, `order_status` | Casing and whitespace inconsistencies | Standardized casing, stripped whitespace |
| `payment_method` | Same payment method represented multiple ways (`COD` / `cod` / `Cash on Delivery`) | Standardized casing, manually merged equivalent labels |
| `delivery_time` | Mixed units (`"35"` vs `"35 min"` vs `"24.5 mins"`), impossible negative values, unrealistic outliers (up to 295 minutes) | Stripped units, converted to numeric, treated negative/unrealistic values (>90 min) as missing, filled with median |
| `order_value` | Multiple currency notations (`₹`, `Rs.`, trailing `/-`), missing values stored as text | Stripped all currency notations, converted to numeric, filled missing with median |
| `rating` | Mixed text/numeric formats (`"5 stars"` vs `"4"`), and an ambiguous `0` value | Stripped text suffixes, converted to numeric; treated `0` as "not rated" rather than a genuine zero-star rating, since food delivery platforms don't allow a true 0-star score |
| `order_date` | Multiple date formats in one column | Parsed with `pd.to_datetime(errors='coerce')`, unparseable rows treated as missing |
| Duplicate rows | Exact duplicate orders present | Removed with `drop_duplicates()` |

## Key Questions Explored
- Which restaurants receive the most orders?
- Which cuisine type has the highest average order value?
- How does delivery time vary across cities?
- What proportion of orders are delivered, cancelled, or returned?
- Is there a relationship between delivery time and customer rating?
- How does order volume trend across the year?

## Key Takeaway: Ambiguous Values Need Judgment, Not Just Code
The `rating` column's `0` values were the most interesting cleaning decision in this project — a `0` could mean either "rated zero stars" or "never rated at all." Since food delivery platforms typically don't allow a true zero-star rating, these were treated as missing rather than genuine low ratings. Mechanically cleaning a column is only half the work — interpreting what a value actually represents in the real-world context is the other half.

## Files
- `food_delivery_data.csv` — raw, uncleaned dataset
- `food_delivery_eda.ipynb` — full cleaning, analysis, and visualization notebook

## Author
Naivedh 
