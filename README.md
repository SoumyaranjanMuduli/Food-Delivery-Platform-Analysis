# 🍽️ Food Delivery Platform Analysis — Zomato & Swiggy

> **End-to-end data analysis project** exploring restaurant trends, ratings, cuisines, delivery performance, and city-level insights across **Zomato** and **Swiggy** — using Python, SQL, Excel, Power BI, and Tableau.

---

## 📌 Project Overview

This project combines two major food delivery platform datasets to uncover comparative insights across restaurant ecosystems:

**Zomato** — Multi-city restaurant analysis covering ratings, cuisines, cost trends, and online ordering adoption across India's top cities.

**Swiggy (Hyderabad)** — Web-scraped restaurant data from Hyderabad covering delivery time, cost buckets, cuisine availability, and platform-specific performance patterns.

Together, they answer:

- Which cities and cuisines dominate food delivery platforms?
- How do ratings, votes, cost-for-two, and delivery time relate to each other?
- What separates high-performing restaurants from the rest?
- How does Swiggy's Hyderabad ecosystem compare to Zomato's city-level trends?
- What drives online ordering and table booking adoption?

---

## 🗂️ Repository Structure

```
📦 food-delivery-analysis
 ┃
 ┣ 📁 zomato/
 ┃  ┣ 📄 data dump.sql                               # Raw database dump
 ┃  ┣ 📄 SQL scripts.sql                              # Queries for analysis
 ┃  ┣ 📊 zomato data.xlsx                             # Source dataset (Excel)
 ┃  ┣ 📋 Zomato Objectives.docx                       # Project goals & questions
 ┃  ┣ 📈 zomato restaurants analysis in Excel         # EDA & pivot analysis
 ┃  ┣ 📊 Zomato restaurants analysis dashboard.pbix   # Power BI dashboard
 ┃  ┗ 📊 Zomato Restaurants analysis Tableau.twbx     # Tableau dashboard
 ┃
 ┣ 📁 swiggy/
 ┃  ┣ 📓 SWIGGY_Data_analysis_Project_.ipynb          # Full analysis notebook
 ┃  ┣ 📊 swiggy_data.csv                              # Raw scraped dataset
 ┃  ┗ 📊 swiggy_cleaned_powerbi.csv                   # Cleaned dataset (Power BI ready)
 ┃
 ┗ 📄 README.md
```

---

## 🔧 Tools Used

| Tool / Library | Purpose |
|---|---|
| **MySQL / SQL** | Data extraction, cleaning, and aggregation (Zomato) |
| **Python** | Core language for scraping and EDA (Swiggy) |
| **BeautifulSoup + Requests** | Web scraping from Swiggy |
| **Pandas + NumPy** | Data cleaning and transformation |
| **Matplotlib + Seaborn** | Data visualization |
| **Microsoft Excel** | Exploratory analysis, pivot tables, charts (Zomato) |
| **Power BI** | Interactive BI dashboards (both platforms) |
| **Tableau** | Visual analytics and storytelling (Zomato) |

---

---

# 🔴 Part 1 — Zomato Restaurant Analysis

---

## 📦 Dataset

The dataset contains information on **9,500+ restaurants** across multiple cities including:

- Restaurant name, location, and city
- Cuisine types
- Average cost for two people
- Aggregate rating and number of votes
- Online order and table booking availability
- Restaurant type and listed category

---

## 📊 Dashboards

### Power BI Dashboard
- City-wise restaurant distribution
- Rating breakdown by cuisine type
- Cost vs. rating correlation
- Online order and table booking availability

### Tableau Dashboard
- Geographic spread of restaurants
- Top-performing cuisines and restaurant chains
- Votes and rating trends
- Comparative city-level performance

---

## 🧠 Key Business Questions Answered

1. Which cities have the highest concentration of restaurants?
2. What cuisines get the best ratings on average?
3. Does cost-for-two affect customer ratings?
4. How many restaurants offer online ordering vs. table booking?
5. Which restaurant types (casual, fine dining, etc.) perform best?
6. What are the top-voted restaurants across categories?

---

## 🚀 How to Use — Zomato

### SQL
```sql
-- Load the data dump first
SOURCE data_dump.sql;

-- Then run the analysis queries
SOURCE SQL_scripts.sql;
```

### Excel
- Open `zomato data.xlsx` for the source data
- Open `zomato restaurants analysis in Excel` for pivot tables and charts

### Power BI
- Open `Zomato restaurants analysis dashboard.pbix` in Power BI Desktop
- Refresh data source if needed

### Tableau
- Open `Zomato Restaurants analysis Tableau.twbx` in Tableau Desktop or Tableau Public

---

## 💡 Zomato Key Insights

- **Bangalore** leads in restaurant count, followed by Delhi and Mumbai
- **North Indian** and **Chinese** cuisines are the most listed
- Restaurants with **online ordering** tend to have higher vote counts
- **Cost-for-two** shows weak correlation with rating — value perception varies heavily by city
- Fine dining scores higher ratings on average but lower vote volumes

---

---

# 🟠 Part 2 — Swiggy Restaurant Analysis (Hyderabad)

---

## 📦 Dataset

- **Source**: Swiggy Hyderabad (scraped via BeautifulSoup)
- **Size**: 1,224 restaurants
- **Categories scraped**: Biryani collection · North Indian collection · Top Rated collection

### Columns in the Cleaned Dataset

| Column | Description |
|---|---|
| `Restaurant` | Restaurant name |
| `Cuisine_Types` | All cuisines served (comma-separated) |
| `Rating` | Aggregate rating (1.7 – 5.0) |
| `Rating_Bucket` | Bucketed rating label |
| `Delivery_Time_Mins` | Estimated delivery time in minutes |
| `Delivery_Speed` | Fast / Standard / Slow label |
| `Cost_For_Two` | Average cost for two people (₹) |
| `Cost_Bucket` | Budget / Affordable / Mid-range / Premium |
| `Has_Biryani` | Whether restaurant serves Biryani (Yes/No) |
| `Has_North_Indian` | North Indian available |
| `Has_Chinese` | Chinese available |
| `Has_South_Indian` | South Indian available |
| `Has_Desserts` | Desserts available |
| `Has_Beverages` | Beverages available |
| `Has_Italian` | Italian available |
| `Has_Tandoor` | Tandoor available |
| `Has_Continental` | Continental available |

---

## 🔍 Analysis Performed

### Data Collection
- Scraped 3 Swiggy collection pages across 30 pages each using `requests` + `BeautifulSoup`
- Extracted restaurant name, cuisine type, rating, delivery time, and cost for two from a single compound field

### Data Cleaning
- Parsed the compound `Time` field (e.g. `4.1•29 MINS•₹500 FOR TWO`) into separate columns
- Replaced `--` ratings with `0` and converted to `float`
- Removed currency symbols and units; cast numeric columns correctly
- Dropped duplicates and irrelevant index columns
- Created binary cuisine-availability flags (Yes/No) for 8 cuisines

### Exploratory Data Analysis (EDA)

**Univariate**
- Rating distribution: most restaurants cluster between **3.8 – 4.2**
- Delivery time distribution: peak at **30–35 minutes**, range 18–66 mins
- Cost distribution: most restaurants priced at **₹300 for two**

**Bivariate**
- Rating vs. Cost: weak positive correlation (0.021) — price doesn't strongly predict rating
- Rating vs. Delivery Time: slight negative correlation (−0.2) — faster deliveries tend to rate slightly higher
- Continental-serving restaurants rate marginally higher (3.7 vs 3.6)

**Top 10 Analysis**
- **Top rated**: Earth Craft (5.0), Authentic Belgian Waffles (4.9), Go Foodies (4.8)
- **Most outlets**: Shree Santosh Family Dhaba has the highest number of listings
- **Most expensive**: ITC Kohenur leads price-per-two rankings
- **Most common cuisine**: North Indian (552), Chinese (392), Biryani (347)

---

## 📊 Power BI Dashboard — Swiggy

### How to Build It (2 Minutes)

1. Open **Power BI Desktop**
2. Click **Get Data → Text/CSV** → select `swiggy_cleaned_powerbi.csv`
3. Click **Transform Data** → verify column types → click **Close & Apply**
4. Build these visuals:

| Visual | Fields |
|---|---|
| **KPI Cards** | Total Restaurants · Avg Rating · Avg Delivery Time · Avg Cost For Two |
| **Bar Chart** | Top 10 Cuisines by restaurant count (`Cuisine_Types`) |
| **Donut Chart** | Rating bucket distribution (`Rating_Bucket`) |
| **Donut Chart** | Cost bucket distribution (`Cost_Bucket`) |
| **Bar Chart** | Top 10 Restaurants by `Rating` |
| **Bar Chart** | Delivery Speed breakdown (`Delivery_Speed`) |
| **Scatter Plot** | `Rating` vs `Cost_For_Two` |
| **Slicers** | `Has_Biryani` · `Has_North_Indian` · `Cost_Bucket` · `Rating_Bucket` |

---

## 🚀 How to Run — Swiggy Notebook

```bash
# Clone the repo
git clone https://github.com/yourusername/food-delivery-analysis.git
cd food-delivery-analysis/swiggy

# Install dependencies
pip install pandas numpy matplotlib seaborn beautifulsoup4 requests

# Launch notebook
jupyter notebook SWIGGY_Data_analysis_Project_.ipynb
```

> **Note**: Live web scraping from Swiggy may not work as the site structure has changed since this data was collected. Use the included `swiggy_data.csv` for offline analysis.

---

## 💡 Swiggy Key Insights

- **4.0 is the modal rating** — over 21% of restaurants are rated exactly 4.0
- **North Indian dominates** — present in 552 out of 1,224 restaurants in Hyderabad
- **₹200–₹400 is the sweet spot** — 55% of restaurants fall in this cost range
- **Price doesn't drive ratings** — correlation between cost and rating is near-zero (0.021)
- **Faster delivery slightly correlates with better ratings** (−0.2 correlation)
- **Only 18.3% of restaurants serve Beverages** — significant gap vs food-only listings
- **Italian food is rare** — very few restaurants offer Italian cuisine in this dataset

---

---

# 🔁 Cross-Platform Comparison

| Dimension | Zomato (Multi-City) | Swiggy (Hyderabad) |
|---|---|---|
| **Dataset Size** | 9,500+ restaurants | 1,224 restaurants |
| **Top Cuisine** | North Indian & Chinese | North Indian (552 listings) |
| **Cost–Rating Correlation** | Weak | Near-zero (0.021) |
| **Top City by Volume** | Bangalore | Hyderabad (focused) |
| **Scraping Method** | SQL dump | BeautifulSoup |
| **Dashboard Tools** | Power BI + Tableau | Power BI |
| **Unique Variable** | Online ordering & table booking | Delivery time & speed |

---

## 👤 Author

**[Your Name]**
[LinkedIn](https://linkedin.com/in/yourprofile) · [Portfolio](https://yourportfolio.com) · [Email](mailto:you@email.com)

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

*Data sourced from publicly available Zomato restaurant listings and scraped from Swiggy Hyderabad. Used for educational and analytical purposes only. Not affiliated with Zomato or Swiggy.*
