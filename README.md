# 🛒 Zambia National Retail Intelligence Platform

### *An End-to-End Data Science Project | Retail Analytics · Demand Forecasting · Business Intelligence*

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/XGBoost-ML%20Forecasting-006600?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Plotly-Interactive%20Viz-3F4F75?style=for-the-badge&logo=plotly&logoColor=white"/>
  <img src="https://img.shields.io/badge/Google%20Colab-Ready-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white"/>
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge"/>
</p>

<p align="center">
  <strong>Author:</strong> Given Chinyama &nbsp;|&nbsp;
  <strong>Date:</strong> June 2026 &nbsp;|&nbsp;
  <a href="https://www.linkedin.com/in/given-chinyama-data">LinkedIn</a> &nbsp;|&nbsp;
  <a href="https://github.com/GIVEN-CHINYAMA">GitHub</a>
</p>

---

## 📌 Overview

Zambia's retail sector is undergoing rapid transformation — driven by urbanisation, mobile money adoption, and a growing middle class across cities like Lusaka, Kitwe, Ndola, and Livingstone. Yet the vast majority of retailers still operate without data-driven insight, relying on intuition over analytics.

This project addresses that gap by building a **National Retail Intelligence Platform** — a production-grade, end-to-end data science pipeline that simulates, cleans, analyses, forecasts, and visualises Zambian retail data across 7 cities, 8 store chains, and 24 product categories.

The platform is designed to serve three distinct audiences:

| Audience | Use Case |
|---|---|
| 🏪 Retailers & FMCG distributors | Reduce stockouts, optimise inventory, plan promotions |
| 📊 Data scientists & analysts | Reproducible forecasting and segmentation pipelines |
| 🏛️ Government & trade policy teams | National retail price monitoring and trade analytics |

---

## ✨ Key Features

- **Realistic synthetic dataset** — 80,000 transactions across 7 Zambian cities, population-weighted and seasonally adjusted, all priced in Zambian Kwacha (ZMW)
- **Dual forecasting models** — ARIMA for seasonal trend interpretation and XGBoost for high-accuracy daily demand prediction
- **RFM customer segmentation** — Recency, Frequency, and Monetary analysis combined with K-Means clustering to identify Champions, Loyal Regulars, New Customers, and At-Risk segments
- **Stockout and overstock risk detection** — Rule-based flags combined with Z-score anomaly detection on daily revenue streams
- **Executive BI dashboard** — A 9-panel interactive Plotly dashboard covering revenue, margins, seasonality, promotions, and YoY growth
- **Feature engineering pipeline** — Lag features, rolling averages, seasonal flags, and volatility indicators for ML-ready daily aggregates

---

## 🗂️ Project Structure

```
zambia-retail-intelligence-platform/
│
├── Zambia_National_Retail_Intelligence_Platform.ipynb   # Main notebook (all 10 stages)
│
├── outputs/
│   ├── zambia_retail_dataset.csv           # Raw transaction data (80,000 records)
│   ├── zambia_retail_daily_features.csv    # Engineered daily features for ML
│   ├── zambia_customer_rfm_segments.csv    # Customer RFM scores + cluster labels
│   ├── zambia_stockout_risk.csv            # Product-level stockout risk ranking
│   └── zambia_customer_segments.csv        # Segment profiles (Champions, etc.)
│
├── charts/
│   └── seasonality_analysis.png           # Exported Matplotlib seasonality chart
│
├── requirements.txt                        # Python dependencies
└── README.md
```

---

## 🔬 Methodology — 10-Stage Pipeline

### Stage 1 — Environment Setup
Installation of all required libraries with version pinning. Compatible with Google Colab, Jupyter Lab, and local Python environments.

### Stage 2 — Synthetic Data Generation
Since no unified national retail dataset exists publicly for Zambia, a realistic synthetic dataset is engineered from the ground up using:

- **7 cities** (Lusaka, Kitwe, Ndola, Livingstone, Chipata, Kabwe, Solwezi) with population-weighted sales volumes
- **8 retail chains** across Large Supermarket, Medium Supermarket, Department Store, and Informal Retail formats
- **24 product SKUs** across 9 categories (Staples, Dairy, Protein, Produce, HPC, Telecoms, Beverages, Baby Care, Stationery)
- **Zambia-specific seasonal multipliers** — festive peaks in December (+40%), back-to-school in January (+25%), harvest season in April (+10%)
- **Promotion simulation** — 15% of transactions include a random discount between 5% and 25%
- **Stock lifecycle** — stock-before and stock-after quantities per transaction, with a reorder threshold of 20 units

### Stage 3 — Data Cleaning & Validation
A full data quality audit is performed prior to any analysis:

- Null and missing value checks
- Duplicate transaction ID detection and removal
- Negative revenue and zero-unit transaction filtering
- Statistical summary of all key numeric columns

### Stage 4 — Exploratory Data Analysis (EDA)
Twelve visualisations covering:

- Revenue breakdown by city, product category, store type, and month
- Zambia-specific seasonality patterns (monthly and day-of-week)
- Promotion impact analysis — revenue lift vs. gross margin trade-off

### Stage 5 — Feature Engineering
A daily aggregate table is derived from the transaction data, enriched with:

- Time-based features: day of week, month, quarter, year, day of year, weekend flag, month-start/end flags
- Seasonal flags: festive season (Nov–Dec), back-to-school (Jan, Sep)
- Lag features: 7-day, 14-day, and 30-day lagged revenue
- Rolling statistics: 7-day and 30-day rolling mean and rolling standard deviation (volatility)

### Stage 6 — Demand Forecasting
Two models are built and benchmarked head-to-head:

**ARIMA (2,1,2)** — fitted on monthly aggregated revenue:
- Interpretable seasonal trend decomposition
- 95% confidence intervals on the 6-month test horizon
- Best for executive-level seasonal reporting

**XGBoost Regressor** — fitted on the engineered daily feature set:
- 500 estimators, learning rate 0.05, max depth 6
- Chronological 80/20 train-test split
- Feature importance analysis (top 10 drivers)
- Best for operational daily forecasting

Both models are evaluated on MAE, RMSE, MAPE, and R².

### Stage 7 — Customer Segmentation (RFM + K-Means)
RFM scores are computed for all ~5,000 simulated customers:

- **Recency** — days since last purchase relative to snapshot date
- **Frequency** — total transaction count
- **Monetary** — total revenue generated

K-Means clustering (K=4, selected via elbow method, validated with silhouette score) identifies four segments:

| Segment | Characteristics | Recommended Action |
|---|---|---|
| 💎 Champions | High monetary, high frequency, recent | Loyalty rewards, early access |
| 🔄 Loyal Regulars | Consistent frequency, moderate spend | Upsell and cross-sell campaigns |
| 🌱 New Customers | Low frequency, recent | Onboarding offers, retention incentives |
| 😴 Lost / At-Risk | High recency (not seen recently) | Win-back promotions, churn prevention |

### Stage 8 — Stockout & Overstock Risk Detection
A two-layer risk detection system:

- **Product-level stockout rate** — ranked table of all 24 SKUs by percentage of transactions where stock-after fell below the reorder point
- **Demand anomaly detection** — Z-score method applied to the daily revenue series; days beyond ±2.5 standard deviations are flagged as anomalies

### Stage 9 — Executive BI Dashboard
A 9-panel, fully interactive Plotly dashboard delivered as a single figure:

1. Revenue by city
2. Monthly revenue trend (2022–2024)
3. Top 10 products by revenue
4. Category revenue share (donut chart)
5. Gross margin by category
6. Stockout risk by city
7. Customer segment distribution
8. Promotional vs non-promotional revenue
9. Year-on-year revenue growth

### Stage 10 — Insights, Recommendations & Conclusions
Synthesised business findings with strategic recommendations for retailers, FMCG distributors, and policy makers. Includes a roadmap for future work.

---

## 📊 Key Findings

| # | Finding | Implication |
|---|---|---|
| 1 | Lusaka drives ~38% of national retail revenue | Prioritise Lusaka for flagship stores and distribution hubs |
| 2 | December revenue spikes +40% above baseline | Pre-position stock by October; negotiate supplier capacity in Q3 |
| 3 | Staples (Mealie Meal, Cooking Oil) dominate revenue | Price-sensitive; margin protection requires bulk procurement |
| 4 | Promotions lift volume but compress gross margins | Run promotions selectively on high-volume, low-margin SKUs only |
| 5 | ~25% of SKUs carry elevated stockout risk | Implement automated reorder triggers at item level |
| 6 | Champions segment generates disproportionate value | Launch loyalty programmes targeting this segment immediately |
| 7 | XGBoost achieves strong daily demand forecast accuracy | Deploy ML forecasting to automate purchase order generation |
| 8 | Weekend sales outperform weekdays across all cities | Schedule promotions and delivery windows around Friday–Saturday |

---

## 🛠️ Tech Stack

| Tool | Version | Purpose |
|---|---|---|
| Python | 3.10+ | Core language |
| Pandas | 2.x | Data manipulation |
| NumPy | 1.x | Numerical computation |
| Scikit-learn | 1.x | Preprocessing, K-Means, metrics |
| XGBoost | 2.x | Gradient-boosted demand forecasting |
| Statsmodels | 0.14+ | ARIMA time-series modelling |
| Plotly | 5.x | Interactive charts and BI dashboard |
| Matplotlib | 3.x | Static charts and seasonality plots |
| Seaborn | 0.13+ | Statistical visualisation styling |
| Kaleido | 0.2+ | Exporting Plotly charts to PNG/PDF |

---

## ⚡ Quick Start

### Option A — Google Colab (recommended)

Click the badge below to open the notebook directly in Google Colab — no local installation required:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/GIVEN-CHINYAMA/zambia-retail-intelligence-platform/blob/main/Zambia_National_Retail_Intelligence_Platform.ipynb)

### Option B — Local installation

**1. Clone the repository**
```bash
git clone https://github.com/GIVEN-CHINYAMA/zambia-retail-intelligence-platform.git
cd zambia-retail-intelligence-platform
```

**2. Create and activate a virtual environment**
```bash
python -m venv venv
source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Launch Jupyter**
```bash
jupyter lab
```

**5. Open and run**

Open `Zambia_National_Retail_Intelligence_Platform.ipynb` and run all cells from top to bottom. The synthetic dataset is generated programmatically — no external data download is needed.

---

## 📦 Requirements

```
pandas>=2.0.0
numpy>=1.24.0
scikit-learn>=1.3.0
xgboost>=2.0.0
statsmodels>=0.14.0
plotly>=5.18.0
matplotlib>=3.7.0
seaborn>=0.13.0
kaleido>=0.2.1
jupyter>=1.0.0
```

Install all at once:
```bash
pip install -r requirements.txt
```

---

## 📁 Output Files

After running all cells, the following CSV files are saved to the working directory:

| File | Description | Rows |
|---|---|---|
| `zambia_retail_dataset.csv` | Full cleaned transaction dataset | ~80,000 |
| `zambia_retail_daily_features.csv` | Daily aggregates with engineered ML features | ~1,065 |
| `zambia_customer_rfm_segments.csv` | Customer-level RFM scores and cluster labels | ~5,000 |
| `zambia_stockout_risk.csv` | Product stockout risk ranking | 24 |
| `zambia_customer_segments.csv` | Cluster profile summary (4 segments) | 4 |

---

## 🚀 Roadmap — Future Development

- [ ] **SQL data warehouse** — migrate outputs to a PostgreSQL star schema (fact_sales + dimension tables) for scalable querying
- [ ] **Streamlit web app** — live interactive dashboard deployable to Streamlit Cloud
- [ ] **Power BI integration** — connect SQL warehouse via ODBC for executive-level Power BI reports
- [ ] **Economic indicators layer** — incorporate real ZamStats inflation data, Bank of Zambia ZMW/USD exchange rates, and ZERA fuel prices as model features
- [ ] **Real-time POS data** — API integration with Shoprite Zambia or Pick n Pay POS systems
- [ ] **Geospatial heatmaps** — district-level revenue maps using Zambia administrative shapefiles
- [ ] **LSTM deep learning** — longer-horizon demand forecasting with sequence models
- [ ] **Mobile money signals** — Airtel Money and MTN MoMo transaction volumes as leading demand indicators

---

## 📚 Data Sources & References

All transaction data in this project is **synthetic** and generated programmatically to reflect realistic Zambian retail patterns. The following sources informed the simulation design:

- [Zambia Statistics Agency (ZamStats)](https://www.zamstats.gov.zm/) — Retail Trade Surveys and Consumer Price Index
- [Bank of Zambia](https://www.boz.zm/) — ZMW exchange rate historical data
- [World Bank — Zambia Economic Monitor](https://www.worldbank.org/en/country/zambia) — Macroeconomic context
- [ZERA](https://www.zera.org.zm/) — Zambia Energy Regulation Authority fuel price data

> All data is synthetic and generated for educational and portfolio purposes only. No proprietary or confidential retail data has been used.

---

## 🤝 Contributing

Contributions are welcome. To contribute:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "Add: your feature description"`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

Please open an issue first to discuss any significant changes.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Given Chinyama**
Data Scientist | Zambia

- GitHub: [@GIVEN-CHINYAMA](https://github.com/GIVEN-CHINYAMA)
- LinkedIn: [given-chinyama-data](https://www.linkedin.com/in/given-chinyama-data)

---

<p align="center">
  <i>Built with purpose — equipping Zambian retail with the intelligence it deserves.</i>
</p>

