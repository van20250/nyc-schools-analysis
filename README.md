# 🏫 NYC Schools Data Analysis & Cleaning Project

## 📌 Overview
This repository contains a collection of projects focused on analyzing and cleaning datasets from the **New York City public school system**.  
It integrates work on:  
1. **SAT Results Cleaning & Outlier Removal**  
2. **Brooklyn School Data Analysis**  
3. **NYC School Incidents Analysis**  
4. **General NYC Schools Demographics & Performance Analysis**  

The goal is to produce **high-quality, cleaned datasets** and **insightful analytics** to better understand school performance, demographics, and safety across NYC boroughs.

---

## 📂 Project Structure
├── data/ # Raw and cleaned datasets
├── notebooks/ # Jupyter Notebooks for exploration & visualization
├── scripts/ # Python scripts for ETL, cleaning, and analysis
├── outputs/ # Charts, summaries, and reports
├── README.md # This documentation
└── requirements.txt # Python dependencies


---

## 📊 Datasets & Data Cleaning

### 1️⃣ SAT Results Cleaning & Outlier Removal
**Source:** NYC Public High Schools SAT Scores Dataset  

**Cleaning Steps:**
- Renamed columns to consistent `snake_case`.
- Removed irrelevant or duplicate columns:
  - `sat_critical_readng_avg_score` (duplicate with typo)
  - `internal_school_id` (system-generated)
  - `contact_extension` (not relevant)
- Converted percentages (graduation & attendance rates) from `"85%"` to numeric values.
- Handled missing values by converting to `NaN` instead of dropping rows.
- Removed statistical outliers using the **IQR method** for:
  - `sat_critical_reading`
  - `sat_math`
  - `sat_writing`
  - `graduation_rate`
  - `attendance_rate`

**Before vs. After Outlier Removal:**

| Metric                  | Before Cleaning | After Cleaning |
|------------------------|----------------|----------------|
| Total Rows             | 450            | 437            |
| SAT Critical Reading   | 180–900        | 200–800        |
| SAT Math               | 180–950        | 200–800        |
| SAT Writing            | 150–920        | 200–800        |
| Graduation Rate (%)    | 0–150%         | 50–100%        |
| Attendance Rate (%)    | 0–140%         | 60–100%        |

**Final Schema:**

| Column               | Type   | Description |
|----------------------|--------|-------------|
| dbn                  | TEXT   | Unique school code |
| school_name          | TEXT   | School name |
| sat_critical_reading | INT    | Avg score (200–800) |
| sat_math             | INT    | Avg score (200–800) |
| sat_writing          | INT    | Avg score (200–800) |
| graduation_rate      | FLOAT  | % graduated (0–100) |
| attendance_rate      | FLOAT  | % attendance (0–100) |
| academic_tier_rating | INT    | School tier (1–4, nullable) |

---

### 2️⃣ Brooklyn School Data Analysis
**Objective:** Analyze Brooklyn high schools for performance and enrollment trends.

**Key Steps:**
- Filtered dataset for **Brooklyn schools only**.
- Normalized column names.
- Counted **unique schools** and **Grade 9 entry offerings**.
- Summarized **average student count per borough**.
- Created **bar charts** showing school distribution by borough.

**Insights:**
- Brooklyn has the **highest number of schools**.
- A large portion of Brooklyn schools offer Grade 9 entry.
- Enrollment varies significantly between boroughs.

---

### 3️⃣ NYC School Incidents Analysis
**Objective:** Understand incident patterns in NYC schools.

**Data Cleaning:**
- Standardized column names (lowercase, underscores, no special characters).
- Used **Google Sheets formulas** for quick cleaning:
  ```excel
  =LOWER(REGEXREPLACE(SUBSTITUTE(A1, " ", "_"), "[^a-z0-9_]", ""))

Analysis Performed:

Counted total & unique schools.
Summed incident types: major_n, oth_n, nocrim_n, prop_n, vio_n.
Found the most frequent incident type.
Calculated % of incidents in the Bronx.
Created pivot tables & charts for borough-level distribution.

Insights:
Bronx showed higher incident rates compared to its number of schools.
Some schools reported zero incidents — possible underreporting.
Certain years had spikes in specific incident types.

4️⃣ General NYC Schools Analysis (PostgreSQL + Python)
Focus: Demographic & performance queries.

Key Analysis:

Count schools by borough:
SELECT borough, COUNT(*) AS school_count
FROM nyc_schools.high_school_directory
GROUP BY borough;
Average % of English Language Learners (ELL) by borough.

Joined datasets on dbn to merge demographics with performance.

🛠️ Technologies Used

Python 3.x (Pandas, Matplotlib, Psycopg2/SQLAlchemy)

PostgreSQL for structured storage & querying

Google Sheets for quick cleaning & analysis

Jupyter Notebook for interactive exploration

🚀 How to Run

Clone the repository
git clone https://github.com/your-username/nyc-schools-analysis.git
cd nyc-schools-analysis

Set up environment
python3 -m venv venv
source venv/bin/activate  # Mac/Linux
venv\Scripts\activate     # Windows
pip install -r requirements.txt

Run cleaning scripts
python scripts/clean_sat_data.py
Explore data in Jupyter

📈 Example Outputs
Charts: School counts per borough, incident distribution, SAT score histograms
Tables: Borough-level summaries, top schools by performance, outlier-free SAT results

📌 Why This Project Matters

Ensures data integrity for NYC school performance analysis.
Provides actionable insights for policymakers and educators.
Creates a centralized, cleaned dataset ready for ML or BI tools.

📌 Future Improvements

Automate cleaning workflows using Python & Google Apps Script.
Build interactive dashboards with Tableau or Power BI.
Integrate with BigQuery for large-scale queries.
Apply predictive modeling for performance forecasting.

📜 License
This project is licensed under the MIT License.
