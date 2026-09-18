[CarDekho_Car_Market_Trends_README.md](https://github.com/user-attachments/files/32390509/CarDekho_Car_Market_Trends_README.md)

# Car Market Trends Analysis — CarDekho Dataset (India)

A used-car listings dataset sourced from **CarDekho**, India's leading online
automotive marketplace. It captures key specifications, usage history, and pricing
information for **301 pre-owned vehicles**, making it well-suited for used-car
price prediction, depreciation analysis, and Indian automotive market research.

---

## File

| Property | Value |
|----------|-------|
| Filename | `1776311302-P3-Car Market Trends Analysis with Car Dekho Data(in).csv` |
| Rows | 301 |
| Columns | 9 |
| Missing Values | None |
| Source | CarDekho (India) |
| Price Unit | Indian Rupees — **Lakh INR** (1 Lakh = ₹1,00,000) |

---

## Column Descriptions

| Column | Type | Range / Values | Description |
|--------|------|----------------|-------------|
| `Car_Name` | String | 98 unique models | Model name of the car (e.g. `city`, `swift`, `fortuner`) |
| `Year` | Integer | 2003 – 2018 | Manufacturing year of the car |
| `Selling_Price` | Float | 0.10 – 35.00 | **Target.** Asking / selling price of the used car (Lakh INR) |
| `Present_Price` | Float | 0.32 – 92.60 | Current ex-showroom price of the same model when new (Lakh INR) |
| `Kms_Driven` | Integer | 500 – 5,00,000 | Total kilometres driven by the car |
| `Fuel_Type` | Categorical | Petrol, Diesel, CNG | Fuel type of the engine |
| `Seller_Type` | Categorical | Dealer, Individual | Whether the seller is a dealership or a private individual |
| `Transmission` | Categorical | Manual, Automatic | Gearbox type |
| `Owner` | Integer | 0, 1, 3 | Number of previous owners (0 = first owner) |

---

## Target Variable — `Selling_Price`

The asking price of the used car in **Lakh INR**.

| Statistic | Value |
|-----------|------:|
| Minimum | ₹0.10 L |
| 25th Percentile | ₹0.90 L |
| Median | ₹3.60 L |
| Mean | ₹4.66 L |
| 75th Percentile | ₹6.00 L |
| Maximum | ₹35.00 L |
| Std Dev | ₹5.08 L |

> The distribution is right-skewed — most cars sell below ₹6 L, but a few
> premium/luxury vehicles push the mean above the median. Consider a
> **log transform** of `Selling_Price` for linear models.

---

## Key Statistics

### Numeric Features

| Feature | Min | Mean | Median | Max | Std Dev |
|---------|----:|-----:|-------:|----:|--------:|
| `Year` | 2003 | 2013.6 | 2014 | 2018 | 2.9 |
| `Selling_Price` (L) | 0.10 | 4.66 | 3.60 | 35.00 | 5.08 |
| `Present_Price` (L) | 0.32 | 7.63 | 6.40 | 92.60 | 8.64 |
| `Kms_Driven` | 500 | 36,947 | 32,000 | 5,00,000 | 38,887 |
| `Owner` | 0 | 0.04 | 0 | 3 | 0.25 |

### Categorical Distributions

**Fuel Type**

| Fuel Type | Count | % |
|-----------|------:|--:|
| Petrol | 239 | 79.4% |
| Diesel | 60 | 19.9% |
| CNG | 2 | 0.7% |

**Seller Type**

| Seller Type | Count | % |
|-------------|------:|--:|
| Dealer | 195 | 64.8% |
| Individual | 106 | 35.2% |

**Transmission**

| Transmission | Count | % |
|--------------|------:|--:|
| Manual | 261 | 86.7% |
| Automatic | 40 | 13.3% |

**Previous Owners**

| Owners | Count | % | Meaning |
|--------|------:|--:|---------|
| 0 | 290 | 96.3% | First owner |
| 1 | 10 | 3.3% | Second owner |
| 3 | 1 | 0.3% | Fourth owner |

### Listings by Year

| Year | Listings | | Year | Listings |
|------|----------|-|------|----------|
| 2003 | 2 | | 2011 | 19 |
| 2004 | 1 | | 2012 | 23 |
| 2005 | 4 | | 2013 | 33 |
| 2006 | 4 | | 2014 | 38 |
| 2007 | 2 | | 2015 | 61 |
| 2008 | 7 | | 2016 | 50 |
| 2009 | 6 | | 2017 | 35 |
| 2010 | 15 | | 2018 | 1 |

### Most Listed Car Models (Top 10)

| Car Model | Listings |
|-----------|--------:|
| City | 26 |
| Corolla Altis | 16 |
| Verna | 14 |
| Fortuner | 11 |
| Brio | 10 |
| Ciaz | 9 |
| Innova | 9 |
| i20 | 9 |
| Grand i10 | 8 |
| Royal Enfield Classic 350 | 7 |

> Note: The dataset also includes **motorcycles** (e.g. Royal Enfield Classic 350),
> not just cars. Filter by `Present_Price` or `Car_Name` if you need cars only.

---

## Derived Features (Recommended)

These columns can be engineered before modelling:

| Feature | Formula | Purpose |
|---------|---------|---------|
| `Car_Age` | `2018 - Year` | Age of the car in years at listing time |
| `Depreciation_Pct` | `(Present_Price - Selling_Price) / Present_Price × 100` | % depreciation from new price |
| `Price_Per_Km` | `Selling_Price / Kms_Driven` | Price efficiency metric |
| `Is_First_Owner` | `Owner == 0` | Binary flag for first-owner vehicles |

---

## Suggested Use Cases

| Task | Target | Approach |
|------|--------|----------|
| **Used car price prediction** | `Selling_Price` | Regression (Random Forest, XGBoost, Linear) |
| **Depreciation analysis** | `Present_Price - Selling_Price` | EDA, regression |
| **Price classification** (budget/mid/premium) | `Selling_Price` bins | Multi-class classification |
| **Mileage impact study** | `Selling_Price` vs `Kms_Driven` | Correlation, scatter analysis |
| **Fuel type price comparison** | `Selling_Price` by `Fuel_Type` | Group comparison, ANOVA |
| **Dealer vs individual pricing** | `Selling_Price` by `Seller_Type` | Hypothesis testing |
| **Transmission premium analysis** | `Selling_Price` by `Transmission` | EDA, statistical test |

---

## Notes

- All prices are in **Lakh INR** (₹1 Lakh = ₹1,00,000 ≈ $1,200 USD).
- **`Present_Price`** is the current new ex-showroom price of the same model —
  useful for computing depreciation and as a strong baseline feature.
- **`Owner = 0`** means the current seller is the **first owner** (96.3% of listings).
- **`Kms_Driven`** contains an extreme outlier at 5,00,000 km — consider capping or
  log-transforming for regression models.
- The dataset includes a small number of **two-wheelers** (e.g. Royal Enfield Classic 350,
  activa) — handle these separately if doing car-only analysis.
- **No missing values** — the dataset is clean and ready to use.

---

## Quick Load (Python)

```python
import pandas as pd

df = pd.read_csv("1776311302-P3-Car Market Trends Analysis with Car Dekho Data(in).csv")

print(df.shape)   # (301, 9)
print(df.dtypes)

# Engineer useful features
df["Car_Age"]           = 2018 - df["Year"]
df["Depreciation_Pct"]  = ((df["Present_Price"] - df["Selling_Price"])
                            / df["Present_Price"] * 100).round(2)
df["Is_First_Owner"]    = (df["Owner"] == 0).astype(int)

# Encode categoricals
df = pd.get_dummies(df, columns=["Fuel_Type", "Seller_Type", "Transmission"],
                    drop_first=True)

# Features and target
X = df.drop(columns=["Selling_Price", "Car_Name"])
y = df["Selling_Price"]

print(X.shape)   # (301, ...)
```

---

## Dataset Summary Card

| Property | Value |
|----------|-------|
| Records | 301 |
| Features | 9 |
| Target | `Selling_Price` (Lakh INR) |
| Unique Car Models | 98 |
| Year Range | 2003 – 2018 |
| Fuel Types | Petrol (79%), Diesel (20%), CNG (1%) |
| Transmission | Manual (87%), Automatic (13%) |
| Seller Types | Dealer (65%), Individual (35%) |
| Missing Values | None |
| Currency | Indian Rupees — Lakh INR |
