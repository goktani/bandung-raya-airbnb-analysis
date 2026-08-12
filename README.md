# 🏞️ Bandung Raya Airbnb Analysis

**Exploratory Data Analysis & Price Prediction on 572 Airbnb Listings in Greater Bandung, Indonesia**

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-EDA-150458?logo=pandas&logoColor=white)
![Scikit--learn](https://img.shields.io/badge/Scikit--learn-RandomForest-F7931E?logo=scikit-learn&logoColor=white)
![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-20BEFF?logo=kaggle&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📌 About

This project provides a comprehensive exploratory data analysis (EDA) and machine
learning price prediction pipeline on Airbnb accommodation listings across
**Bandung Raya (Greater Bandung)**, West Java, Indonesia — a region known for its
cool mountain climate, heritage architecture, and vibrant culinary scene, and one
of Indonesia's most popular weekend getaway destinations.

The dataset spans **572 unique listings** across 4 administrative regions:

| Region | Description |
|---|---|
| **Kota Bandung** | Urban core (Dago, Cidadap, Cibeunying, Pasteur) |
| **Kabupaten Bandung Barat** | Mountain/nature area (Lembang, Padalarang, Parongpong) |
| **Kabupaten Bandung** | Resort/rural area (Ciwidey, Pangalengan, Soreang) |
| **Kota Cimahi** | City & surrounding borders |

---

## 🎯 Objectives

- Clean and structure raw, semi-formatted scraped data (IDR-formatted prices,
  mixed rating types, skewed review counts)
- Engineer meaningful features from unstructured listing titles (property type,
  Syariah concept, shared rooms)
- Explore regional and property-type price dynamics through visualization
- Build and evaluate a price prediction model, and interpret which features
  matter most

---

## 📂 Repository Structure

```
bandung-raya-airbnb-analysis/
│
├── bandung_airbnb_analysis.ipynb   # Main analysis notebook (Kaggle-ready)
├── data/
│   └── AirBnB_BandungRaya_All.csv  # Consolidated dataset (572 rows)
├── README.md
└── LICENSE
```

> 💡 On Kaggle, the notebook reads the dataset directly from
> `/kaggle/input/datasets/pandaa12/indonesia-airbnb-dataset-bandung-listings/AirBnB_BandungRaya_All.csv`.
> If running locally, update the `path` variable in the first code cell to point
> to your local CSV location.

---

## 🗂️ Dataset

| Column | Description |
|---|---|
| `nama` | Full listing title and accommodation description |
| `harga` | Nightly rate, formatted as IDR text (e.g. `Rp 1,412,207`) |
| `rating` | Average guest rating (1.0–5.0, or `"New"` if no reviews yet) |
| `jumlah_review` | Total number of reviews |
| `link` | Direct URL to the Airbnb listing |
| `wilayah` | Administrative region (Kabupaten/Kota) |

**Source:** [Indonesia Airbnb Dataset: Bandung Raya Accommodation Listings](https://www.kaggle.com/datasets/pandaa12/indonesia-airbnb-dataset-bandung-listings) (Kaggle)
Data was collected via public web scraping; prices reflect listed rates at
extraction time and are subject to change. All trademarks and rights belong to
Airbnb and property hosts.

---

## 🔧 Methodology

### 1. Data Cleaning
- Parsed `harga` from IDR-formatted text into numeric values
- Split `rating` into a numeric column and an `is_new` flag for listings without reviews
- Applied a log(1+x) transform to `jumlah_review` to address strong right-skew

### 2. Feature Engineering
- Extracted `property_type` (Villa, Glamping, Apartment, Room, Hotel, Cabin, Tiny Home, Other) from listing titles via keyword matching
- Derived binary flags: `is_syariah` (Islamic-concept stay), `is_shared` (shared room), `title_length`

### 3. Exploratory Data Analysis
- Regional price distribution (boxplots, median comparisons)
- Property-type price & rating summaries
- Rating vs. price vs. review-count relationships
- Region × property-type average price heatmap
- Correlation analysis across numeric features
- IQR-based outlier detection

### 4. Modeling
- **Random Forest Regressor** predicting nightly price from region, property type,
  rating, review count, and engineered flags
- One-hot encoding for categorical features via `ColumnTransformer` + `Pipeline`
- Evaluated with **MAE**, **RMSE**, and **R²**
- Feature importance ranking to interpret pricing drivers

---

## 📊 Key Visualizations

- Price distribution by region (boxplot & bar chart)
- Listing count and average price by property type
- Rating vs. price scatter plot (bubble size = review count, color = region)
- Region × property-type price heatmap
- Correlation heatmap of numeric features
- Actual vs. predicted price scatter plot
- Top-15 feature importance chart

---

## 🚀 How to Run

### On Kaggle (recommended)
1. Fork/copy the notebook on Kaggle
2. Attach the [dataset](https://www.kaggle.com/datasets/pandaa12/indonesia-airbnb-dataset-bandung-listings) as input
3. Run all cells — no setup required

### Locally
```bash
git clone https://github.com/goktani/bandung-raya-airbnb-analysis.git
cd bandung-raya-airbnb-analysis
pip install -r requirements.txt
jupyter notebook bandung_airbnb_analysis.ipynb
```

**requirements.txt**
```
pandas
numpy
matplotlib
seaborn
scikit-learn
jupyter
```

> Remember to update the CSV `path` variable in the notebook if running outside Kaggle.

---

## 🔑 Key Findings

- Prices vary meaningfully by region — urban Kota Bandung listings differ
  noticeably from nature/resort areas like Lembang and Ciwidey
- Villa and Glamping-type stays tend to command higher average prices than
  standard Room listings
- Rating shows a weak relationship with price, suggesting pricing is driven
  more by location and property type than guest satisfaction scores
- Region and property type consistently rank among the most important
  predictors in the price model

*(Update this section with your notebook's actual output values once run.)*

---

## 💡 Future Work

- Incorporate latitude/longitude for geospatial clustering and hotspot mapping
- Track prices over time to study seasonal/dynamic pricing patterns
- Apply NLP to extract richer amenities (pool, AC, view, etc.) from listing titles
- Experiment with gradient boosting models (XGBoost/LightGBM) for improved accuracy

---

## 📜 License

This project is licensed under the [MIT License](LICENSE). The underlying dataset
belongs to Airbnb and respective property hosts; this repository only contains
analysis code.

---

## 🙋 Contact

If you have questions, suggestions, or want to collaborate, feel free to open an
issue or reach out.

⭐ If you found this project useful, consider giving it a star!
