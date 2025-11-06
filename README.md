# Data-analysis-Project
Bank Analysis 
# Banking Analytics Dashboards

**Project summary**  
This project delivers a comprehensive banking analytics solution with three dashboards: **Transactions**, **Users**, and **Cards**. Each dashboard highlights key KPIs, time and geographic analyses, and visual insights to support operational monitoring and strategic decision-making.

---

## Table of contents
- [Data sources](#data-sources)  
- [Dashboards & KPIs](#dashboards--kpis)  
  - Transactions Dashboard  
  - Users Dashboard  
  - Cards Dashboard  
- [Data model / schema (examples)](#data-model--schema-examples)  
- [Sample SQL queries](#sample-sql-queries)  
- [Sample DAX measures (Power BI)](#sample-dax-measures-power-bi)  
- [Visuals & recommendations](#visuals--recommendations)  
- [Project structure](#project-structure)  
- [How to run / deploy](#how-to-run--deploy)  
- [License](#license)  

---

## Data sources
- `transactions` table — raw transactional logs (one row per transaction).  
- `customers` table — customer demographics and account metadata.  
- `cards` table — card records (limits, brand, status, PIN change date, features).  
*(In your repository include sample CSVs or SQL dumps in `/data`.)*

---

## Dashboards & KPIs

### 1. Transactions Dashboard
**Source:** `transactions` table  
**Key KPIs / figures**
- **Total transactions:** `13.31M`
- **Total amounts:** `571.84M`
- **Transaction types distribution:** Chip / Swipe / Online
- **Average transaction value:** `42.98`
- **Total merchants:** `74.83K`
- **Error rate:** `1.59%`
- **Hourly/time-of-day transaction analysis**
- **Geo map:** total amounts by city

**Important charts**
- Time series (transactions count & amount by hour/day)
- Bar chart: transaction count by type
- Histogram: transaction value distribution
- Top merchants (by volume and amount)
- Map: sum(amount) by city

---

### 2. Users (Customers) Dashboard
**Source:** `customers` table  
**Key KPIs / figures**
- **Total customers:** `2,000`
- **Customers retiring within 2 years:** `67`
- **Average age:** `45 years`
- **Average credit score:** `709.73`
- **Average individual income:** `23.14K`
- **Average total annual income:** `45.72K`
- **Total debt:** `127M`
- Gender distribution (Male / Female)
- Income analysis by age groups
- Customer risk segmentation: Low / Medium / High

**Important charts**
- Age pyramid or bar by age group
- Boxplot / violin of income by age group
- Pie/Donut: gender distribution
- Stacked bar: customers by risk segment
- Table: customers likely to retire (with predicted retirement date)

---

### 3. Cards Dashboard
**Source:** `cards` table  
**Key KPIs / figures**
- **Total cards:** `6,146`
- **Total credit limit:** `88M`
- **Average card limit:** `14.35K`
- **% PIN not changed >6 years:** `78.47%`
- **Chip-enabled cards:** `5,500`
- Analysis of expired cards in last 3 years
- Distribution by type: Debit / Credit / Prepaid
- Distribution by brand: Visa / Mastercard / Amex / Discover

**Important charts**
- Donut: type distribution
- Bar: brand distribution
- Trend: expired cards by month/year (last 3 years)
- Table: cards with long PIN age (over 6 years)

---

## Data model / schema (examples)

### `transactions` (example columns)
- `transaction_id` (PK)
- `customer_id`
- `card_id`
- `merchant_id`
- `transaction_datetime` (timestamp)
- `amount` (decimal)
- `currency`
- `transaction_type` (Chip / Swipe / Online)
- `status` (Success / Failed / Error)
- `city`
- `error_code` (nullable)

### `customers` (example columns)
- `customer_id` (PK)
- `first_name`
- `last_name`
- `gender`
- `birth_date`
- `credit_score` (numeric)
- `monthly_income` (numeric)
- `total_annual_income` (numeric)
- `total_debt` (numeric)
- `retirement_date` (nullable)
- `risk_segment` (Low / Medium / High)

### `cards` (example columns)
- `card_id` (PK)
- `customer_id` (FK)
- `card_type` (Debit / Credit / Prepaid)
- `brand` (Visa / Mastercard / Amex / Discover)
- `credit_limit` (numeric)
- `pin_last_changed_date` (date)
- `chip_enabled` (boolean)
- `expiry_date` (date)
- `status` (Active / Blocked / Expired)

---

## Sample SQL queries

**Total transactions & total amount**
```sql
SELECT
  COUNT(*) AS total_transactions,
  SUM(amount) AS total_amount
FROM transactions;
