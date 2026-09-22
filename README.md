# Data-Quality-Assessment-and-Courier-Shipment-Analytics

## 📌 Project Overview
This project performs an end-to-end Exploratory Data Analysis (EDA) on a DTDC courier/shipment dataset, covering data cleaning, statistical analysis, and visualization to uncover patterns in shipment volume, cost, and delivery behavior across cities and states in India. The project apply Python-based data analysis on a real-world-style logistics dataset.

## 🎯 Objective
To demonstrate comprehensive data analysis skills — from raw data ingestion to actionable insights — by:
- Cleaning and preprocessing a large, real-world-style shipment dataset
- Conducting exploratory analysis
- Visualizing shipment trends, costs, and regional (city/state-wise) traffic patterns
- Deriving business-relevant insights and recommendations for logistics operations

## 🗂️ Dataset Description
- **Source:** [DTDC Courier Dataset (Kaggle)](https://www.kaggle.com/datasets/ravindrasinghrana/dtdc-courier-dataset)
- **Size:** 49,639 rows × 42 original columns
- **Format:** CSV
- **Content:** Simulated courier shipment records including sender/recipient location, shipment weight, tariff/charges, delivery mode, dates (booking, sender, receive, expiry), GSTIN details, value-added services, and consignment metadata.
- **Nature:** Mix of numerical (weights, charges, amounts) and categorical (city, state, mode, relationship, services) features, satisfying capstone dataset requirements (500+ records, 10+ features, mixed data types).

## 🔧 Workflow

### 1. Data Loading & Initial Overview
- Loaded dataset with Pandas; inspected shape, dtypes, and structure using `.shape`, `.info()`, `.head()`

### 2. Data Cleaning & Preprocessing
- **Column pruning:** Removed personally identifying / redundant columns (names, phone numbers, addresses, pincodes) after evaluating their analytical value
- **Missing value treatment:** Investigated *why* each column had missing values (e.g., cross-tab analysis linking Sender Signature to Sender GSTIN, Value Added Services to VAS Charges) before filling — used context-aware placeholders (`'No'` for Yes/No flags, `'Not Applied'` for business ID fields) rather than blind deletion
- **Data type correction:** Converted date columns (`Sender Date`, `Receive Date`, `Expiry Date`) from string to `datetime64`
- **Redundancy removal:** Identified and dropped a duplicate date column (`Date` and `Sender Date` were verified identical) and standardized text columns (casing/whitespace) for consistent categorical grouping
- **Data validation:** Verified logical date ordering (Sender Date ≤ Receive Date ≤ Expiry Date) and checked for duplicate rows (none found)
- **Outlier analysis:** Applied the IQR method to cost-related columns (`Tariff`); investigated flagged records and confirmed they represented legitimate high-weight, Express-mode shipments rather than data errors — retained rather than removed

### 3. Exploratory Data Analysis (EDA)
- Analysis of shipment weight, cost, mode, and geography
- City/state-wise shipment traffic and volume analysis
- Correlation and grouped analysis across numerical and categorical features

### 4. Visualization
- 10+ visualizations using Matplotlib / Seaborn / Plotly, including bar plots, histograms, box plots, and heatmaps

### 5. Insight Generation
- Key findings and business-relevant recommendations documented in Markdown throughout the notebook

## 🛠️ Tools & Technologies
- **Language:** Python
- **Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Plotly
- **Environment:** Jupyter Notebook
- **Version Control:** Git & GitHub

## 📁 Repository Structure
```
├── data/
│   └── Dataset_Generator_for_DTDC.csv
├── notebook/
│   └── DTDC_Shipment_Analysis.ipynb
├── README.md
```
## :pencil2: Author
Aiswarya R Nair
