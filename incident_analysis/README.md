# NYC School Incidents Analysis

This project cleans and explores a dataset of school incidents in NYC using **Google Sheets**.  
The dataset includes school information, location details, and counts of various incident types (major, other, property, violent, etc.).

---

## 📋 Dataset Overview
Columns include:
- `school_year`  
- `building_code`  
- `dbn` (District Borough Number)  
- `location_name`  
- `location_code`  
- `address`  
- `borough` / `borough_name`  
- Incident counts: `major_n`, `oth_n`, `nocrim_n`, `prop_n`, `vio_n`  
- Latitude, longitude, and other location metadata

---

## 🧹 Data Cleaning
Column names were standardized to:
- All lowercase  
- Spaces replaced with underscores  
- Special characters removed  

**Google Sheets Formula for cleaning:**
```excel
=LOWER(REGEXREPLACE(SUBSTITUTE(A1, " ", "_"), "[^a-z0-9_]", ""))

📊 Analysis Performed

1. Total Rows
=COUNTA(A2:A)

2. Unique Schools
=COUNTA(UNIQUE(C2:C))  # Using DBN as unique ID

3. Most Frequent Incident Type
Calculated by summing each incident type column (major_n, oth_n, nocrim_n, prop_n, vio_n)
The incident type with the highest total is the most frequent.

4. % of Incidents in the Bronx
=COUNTIF(Y2:Y, "Bronx") / COUNTA(A2:A)

📊 Example Outputs
Pivot Table – Incident Type Totals
Chart – Incident Distribution by Borough
Chart – Top 10 Schools by Incident Count

🔍 Insights & Anomalies
- Borough distribution shows the Bronx had a higher proportion of incidents than expected relative to its number of schools.
- Found schools with zero reported incidents — worth investigating if this is accurate or under-reporting.
- Identified spikes in specific incident types in certain years.

📂 Files
dataset.csv – Raw dataset (if public)
dataset_cleaned.csv – Dataset with cleaned column names
analysis_sheets_link.txt – Link to Google Sheets with calculations

🚀 How to Use
Open the dataset in Google Sheets.
Apply the cleaning formula to headers.

Use the provided formulas to compute:
Total rows
Unique schools
Most frequent incident type
Bronx incident percentage
Create Pivot Tables and charts for visual insights.

📌 Future Improvements
Automate data cleaning with Google Apps Script
Build a Data Studio / Looker dashboard for visualization
Integrate with BigQuery for scalable analysis

📜 License
This project is released under the MIT License.

