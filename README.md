## Data Cleaning Practice: E-Commerce Orders Dataset

### Overview
This project uses a synthetic, intentionally messy e-commerce orders dataset
(`messy_ecommerce_data.csv`, ~35,000 rows, 18 columns) to practice real-world
data cleaning workflows in Microsoft Excel.

### Dataset Columns
| Column | Description |
|---|---|
| order_id | Unique order identifier (some missing) |
| customer_id | Customer identifier |
| customer_name | Customer full name (inconsistent casing/whitespace) |
| customer_email | Customer email (some invalid/placeholder values) |
| customer_phone | Phone number (multiple formats) |
| product_name | Product purchased |
| category | Product category (typos, casing, whitespace variants) |
| quantity | Units ordered (text numbers, negatives, outliers) |
| unit_price | Price per unit (mixed currency symbols/formats) |
| discount_percent | Discount applied (some invalid >100%) |
| order_date | Order date (six+ different date formats) |
| ship_city / ship_state / ship_country | Shipping location (inconsistent naming) |
| payment_method | Payment type (casing/abbreviation inconsistencies) |
| order_status | Order status (casing/typo variants) |
| rating | Customer rating 1–5 (some out of range, many blank) |
| review_text | Free-text review (HTML tags, extra whitespace, blanks) |

### Known Data Quality Issues
- **Duplicates**: exact duplicate rows and near-duplicates (e.g. trailing whitespace)
- **Missing values**: blanks and placeholder junk (`N/A`, `NULL`, `-`, `unknown`) scattered across most columns; some fully blank rows
- **Inconsistent text formatting**: mixed case, extra whitespace, spelling variants (e.g. "Electronics" vs "Electroincs" vs "electronics ")
- **Inconsistent categorical values**: multiple representations of the same country/payment method/status
- **Date format chaos**: `YYYY-MM-DD`, `MM/DD/YYYY`, `DD-MM-YYYY`, `DD Mon YYYY`, `Month DD, YYYY`, and Unix timestamps in the same column; some future/impossible dates
- **Numeric formatting issues**: prices stored as text with currency symbols/commas, negative prices/quantities, quantities spelled out as words
- **Invalid ranges**: discounts over 100%, ratings outside 1–5
- **Referential issues**: missing order IDs

### Cleaning Plan / Steps
1. Remove exact and near-duplicate rows
2. Standardize text casing and trim whitespace across all text columns
3. Normalize categorical values (category, country, payment method, status) into a consistent set of labels
4. Parse and standardize all date formats into a single `YYYY-MM-DD` format; flag/handle impossible dates
5. Clean numeric fields: strip currency symbols/commas from price, convert text quantities to numbers, handle negative values
6. Handle missing values: decide per-column whether to drop, impute, or flag
7. Validate ranges: cap/flag discounts >100% and ratings outside 1–5
8. Handle missing order IDs and fully blank rows
9. Document all transformations applied and produce a cleaned dataset