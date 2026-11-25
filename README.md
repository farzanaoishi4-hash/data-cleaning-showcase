# Data Cleaning Showcase: Messy E-commerce Sales

Data quality project: profiling, cleaning and validating messy e-commerce sales data using Python, pandas and Jupyter, with documented decisions.

## Dataset
[Messy E-commerce Sales Data on Kaggle](https://www.kaggle.com/datasets/kandeeldev/messy-e-commerce-sales-data): 103 rows, 11 columns.

## Problems found
- Column names with leading spaces
- 3 duplicate Order_IDs (only 1 was an exact copy)
- 32 missing cells (Category, Quantity, Price, Total)
- Text inside number columns (for example "abd", "four hundred", "300$", "4a")
- Negative quantities and prices, and one price outlier (10000)
- Mixed and invalid dates, and 3 orders far outside the Nov 2024 to Nov 2025 range
- Inconsistent spelling: 9 variants of 5 categories, "shoes" vs "Shoes"
- 8 products labelled with the wrong category (for example Yoga Mat as Electronics)
- 5 totals that did not equal Quantity x Price (all exactly 30% too low)

## What I did
- Standardized column names and text spelling
- Removed duplicates using Order_ID as the business key
- Rescued 3 obvious values (300$, four hundred, 4a); set unrecoverable ones to missing
- Removed impossible values and 1 outlier (IQR rule)
- Parsed two date formats; flagged 4 suspect dates instead of inventing values
- Rebuilt categories from a product lookup table (16 fixes)
- Filled 7 quantities and 9 prices with the median and added flag columns
- Recalculated Total as Quantity x Price
- Validated the result with automated checks

## Results
| Check | Before | After |
|---|---|---|
| Rows | 103 | 100 |
| Duplicate Order_IDs | 3 | 0 |
| Missing cells | 32 | 1 |
| Text inside Quantity/Price | 5 | 0 |
| Zero/negative Quantity or Price | 3 | 0 |
| Price outliers (IQR rule) | 1 | 0 |
| Spellings of Category | 9 | 5 |
| Spellings of Product | 21 | 20 |
| Total does not match Qty x Price | 5 | 0 |
| Unreadable/missing dates | 2 | 1 |

## Assumptions and limits
- Imputed values are estimates; use the `quantity_imputed` and `price_imputed` flags to exclude them.
- The 30% gap in 5 totals could be a real discount, but the data has no discount column.
- The expected order window (Nov 2024 to Nov 2025) is inferred from the data, not confirmed by a data owner.
- The one unreadable date ("abc") stays missing.

## Tools
Python, pandas, Jupyter Notebook, VS Code, Git

## How to run
1. Create an environment: `py -m venv .venv`, then activate it
2. Install: `pip install -r requirements.txt`
3. Open `notebooks/cleaning.ipynb` and choose Run All

## Author
Syeda Farzana Faruque ([LinkedIn](https://www.linkedin.com/in/syeda-farzana-faruque-32563a121/))