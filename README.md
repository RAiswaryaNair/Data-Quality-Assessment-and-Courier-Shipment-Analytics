# Data Quality Assessment and Courier Shipment Analytics

## 📌 Project Overview
This project performs an end-to-end Exploratory Data Analysis (EDA) on a DTDC courier shipment dataset (49,639 shipments). It covers data cleaning, statistical analysis and visualization to understand **risk allocation, shipment cost and pricing, delivery time, and state-wise shipment traffic** across India. The analysis is done in Python using Pandas, Matplotlib, Seaborn and Plotly, and is written as a story: each section poses business questions and answers them with evidence.

## 🎯 Objective
To demonstrate a complete data analysis workflow, from raw data to business insight, by:
- Cleaning and validating a large shipment dataset, with every cleaning decision backed by a check
- Running univariate, bivariate and multivariate analysis using `groupby`, pivot tables, crosstabs and correlation
- Visualizing cost, pricing, delivery and geographic patterns
- Turning the findings into practical recommendations for courier operations

## 🗂️ Dataset Description
- **Source:** [DTDC Courier Dataset (Kaggle)](https://www.kaggle.com/datasets/ravindrasinghrana/dtdc-courier-dataset)
- **Size:** 49,639 rows × 42 original columns (33 after cleaning)
- **Format:** CSV
- **Content:** Origin/destination, sender and recipient city/state, shipment weights (actual, volumetric, chargeable), tariff and value-added-service (VAS) charges, shipping mode, risk surcharge, consignment type, GSTIN details, and booking, receive and expiry dates
- **Coverage:** 22 sender states and 36 sender cities
- **Mix of types:** numerical (weights, charges, amounts), categorical (mode, state, VAS, risk, consignment type) and date columns

## 🔧 Workflow

### 1. Data Loading & Initial Overview
Loaded the dataset with Pandas and inspected it using `.shape`, `.info()`, `.head()`, `.tail()` and `.describe()`.

### 2. Data Cleaning & Preprocessing
- **Column pruning:** Dropped personal identifiers and redundant columns (names, phone numbers, addresses, pincodes) after checking their analytical value.
- **Missing values:** Investigated *why* values were missing before filling them, using crosstabs. For example, Sender Signature is always present when a Sender GSTIN exists, and Value Added Services is missing exactly where VAS Charges = 0. Fills were meaningful placeholders (`No` for Yes/No flags, `Not applied` for GSTIN, `None` for VAS), not blind deletion.
- **Data types:** Converted date columns to `datetime64`.
- **Redundancy:** Verified `Date` and `Sender Date` were identical and dropped one.
- **Validation:** Checked logical date order (Sender Date ≤ Receive Date ≤ Expiry Date) and found no violations. No duplicate rows were found.
- **Standardization:** Trimmed whitespace and standardized text casing so categories group correctly.
- **Outliers:** Applied the IQR method to Tariff (1,112 rows, about 2.2%, flagged). Investigation showed these are legitimate high-weight, Express-mode shipments, so they were **retained**, not removed.

### 3. Exploratory Data Analysis
The EDA is organized as four themed sections, each answering business questions:

| Section | Questions answered |
|---|---|
| **6.1 Risk Allocation** | Who bears shipment risk? Does consignment type or VAS change it? |
| **6.2 Shipment Cost** | What does a typical shipment cost? Which mode costs more? How does weight affect tariff? How strongly does tariff drive total amount? How much do VAS contribute? |
| **6.3 Delivery Time** | How long do deliveries take? Does Mode or State affect it? |
| **6.4 Geographic Traffic** | Which states generate the most volume, and how concentrated is it? |

### 4. Visualization
13 visualizations using Matplotlib, Seaborn and Plotly: pie charts, histograms, a box plot, bar charts, a grouped Plotly bar chart, scatter plots and heatmaps (correlation matrix and state × mode).

### 5. Insight Generation
Every chart or table is followed by a written insight backed by numbers. Claims were checked against the data before being written down, and null results (for example, delivery time not depending on Mode) are reported as findings.

## 🔍 Key Findings
- **Risk:** 98.9% of shipments have the Carrier bearing the risk surcharge. The Owner bears it in only 547 shipments (1.1%), and only for documents (Dox) with no value-added service.
- **Cost:** Total Amount is right-skewed (median about 478, mean about 508, range 23 to 1,481).
- **Mode and price:** Median Total Amount is about 731 for Express, 570 for Air Cargo and 413 for Surface. Surface carries 59.8% of all shipments, about three times as many as either other mode.
- **Weight and tariff:** Chargeable Weight always equals Volumetric Weight, so pricing follows package size. Weight and Tariff correlate at 0.82, and Mode sets the price per kg, producing three distinct pricing bands.
- **Tariff and total:** Total Amount equals Tariff plus VAS Charges exactly, so Tariff drives almost the entire bill (correlation 0.98).
- **VAS:** Cod is chosen in 59.6% of shipments and about 20.6% use no VAS. Selection is independent of shipping Mode. When a VAS is chosen, it adds a median of about 17% to the total cost.
- **Delivery time:** All deliveries take 1 to 5 days (average about 3) and show no meaningful relationship with Mode or State. Express averages the same ~3 days as Surface despite costing about 77% more at the median.
- **Geography:** The top 10 sender states account for 67% of shipments. Maharashtra (6,934) and Uttar Pradesh (5,466) lead, followed by a tight middle group and an evenly spread bottom tier.

## 💡 Business Recommendations
TBD

## 🛠️ Tools & Technologies
- **Language:** Python
- **Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Plotly
- **Environment:** Jupyter Notebook
- **Version Control:** Git & GitHub

## ▶️ How to Run
1. Clone the repository.
2. Install the libraries: `pip install pandas numpy matplotlib seaborn plotly jupyter`
3. Open the notebook in the `notebook/` folder.
4. Make sure the CSV path in the data-loading cell points to `data/Dataset_Generator_for_DTDC.csv`.
5. **Download the banner image.** The notebook's title cell displays `logo.png`, which is stored in the [`image/`](image) folder. Download it and place it in the same folder as the notebook (or change the image path in the first cell to `../image/logo.png`). Without it, the banner will not display, but the analysis still runs.
6. Run **Kernel → Restart & Run All**.

## 📁 Repository Structure
```
├── data/
│   └── Dataset_Generator_for_DTDC.csv     # original dataset (as downloaded)
├── notebook/
│   └── DTDC_Shipment_Analysis.ipynb       # full analysis notebook
├── image/                                 # banner image (logo.png) used in the notebook title
├── Cleaned_DTDC_Data.xlsx                 # dataset after cleaning and preprocessing
├── README.md
```

## ✏️ Author
Aiswarya R Nair
