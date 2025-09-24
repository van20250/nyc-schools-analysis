NYC Schools SAT Results – Data Cleaning and Outlier Removal Project

Overview
This project focuses on cleaning and processing NYC public high schools’ SAT results dataset.
The dataset contains performance metrics such as SAT scores, graduation rates, and attendance rates.

The final cleaned dataset is stored in:
Local CSV: nyc_schools_sat_cleaned.csv
PostgreSQL Database: nyc_schools.sumi_sat_results_cleaned

Data Cleaning Steps
1. Initial Cleaning
Renamed columns to consistent snake_case format.
Removed irrelevant columns:
sat_critical_readng_avg_score → Duplicate with typo.
internal_school_id → Synthetic system-generated ID.
contact_extension → Not relevant to analysis.
pct_students_tested → Converted from % to numeric but not included in final schema due to inconsistency.
academic_tier_rating → Kept if available, but not used in SAT performance analytics.
Converted percentage columns (e.g., graduation_rate, attendance_rate) from strings like "85%" to numeric values.
Handled missing values: Converted to NaN instead of deleting whole rows to preserve data.

2. Outlier Removal (Final Cleaning Step)
We used the IQR (Interquartile Range) method to detect and remove extreme values in:
sat_critical_reading
sat_math
sat_writing
graduation_rate
attendance_rate

Before vs. After Outlier Removal

Metric	Before Cleaning	After Cleaning

Total Rows	450	437
SAT Critical Reading Avg	180 – 900	200 – 800
SAT Math Avg	180 – 950	200 – 800
SAT Writing Avg	150 – 920	200 – 800
Graduation Rate (%)	0% – 150%	50% – 100%
Attendance Rate (%)	0% – 140%	60% – 100%

📌 Outliers such as SAT scores above 800 or rates above 100% were removed to keep data within logical ranges.

Final Data Schema

Column Name	Type	Description
dbn	TEXT	Unique school code (District Borough Number).
school_name	TEXT	Official name of the school.
sat_critical_reading	INTEGER	Avg SAT Critical Reading score (200–800).
sat_math	INTEGER	Avg SAT Math score (200–800).
sat_writing	INTEGER	Avg SAT Writing score (200–800).
graduation_rate	FLOAT	% of students who graduated (0–100).
attendance_rate	FLOAT	% of students attending school regularly (0–100).
academic_tier_rating	INTEGER	School’s performance tier (1–4), may be null.

How to Run

Load the raw SAT dataset.
Run clean_sat_data.py to:
Normalize column names.
Remove irrelevant columns.
Convert percentage values to numbers.
Remove statistical outliers.
Save the cleaned dataset.

View results in:

CSV file: nyc_schools_sat_cleaned.csv
Database table: nyc_schools.sumi_sat_results_cleaned (PostgreSQL, schema: nyc_schools).

Why This Matters

Ensures all SAT scores are within valid ranges.
Removes unrealistic graduation/attendance rates.
Produces a reliable dataset for educational performance analysis.
Preserves data integrity by keeping valid records instead of dropping too much.
