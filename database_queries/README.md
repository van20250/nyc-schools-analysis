# NYC Schools Data Analysis

## 📌 Overview
This project analyzes NYC school data to answer various educational insights questions, such as:
- Average percentage of English Language Learners (ELL) in each borough.
- Total number of schools by borough.
- Other demographic and performance-based statistics.

The data is stored in a PostgreSQL database and queried using SQL via Python (pandas + psycopg2/SQLAlchemy).

## 📂 Project Structure
├── data/ # Raw and processed data files
├── notebooks/ # Jupyter notebooks for exploration
├── scripts/ # Python scripts for ETL and analysis
├── README.md # Project documentation (this file)
└── requirements.txt # Python dependencies

## ⚙️ Installation & Setup

### 1️⃣ Clone the repository
```bash
git clone https://github.com/your-username/nyc-schools-analysis.git
cd nyc-schools-analysis
2️⃣ Create & activate a virtual environment

python3 -m venv venv
source venv/bin/activate  # Mac/Linux
venv\Scripts\activate     # Windows

3️⃣ Install dependencies
pip install -r requirements.txt

🗄 Database Connection
Make sure you have your PostgreSQL database running and update the connection details in config.py:
DB_HOST = "localhost"
DB_NAME = "nyc_schools"
DB_USER = "your_username"
DB_PASS = "your_password"

📊 Example Queries
Count schools by borough
SELECT borough, COUNT(*) AS school_count
FROM nyc_schools.high_school_directory
GROUP BY borough;

English Language Learners (ELL) by borough
SELECT borough, ell_percent
FROM school_demographics
JOIN high_school_directory USING (dbn);

🚀 Running the Analysis
python scripts/analyze_schools.py
Or run the Jupyter notebooks in the notebooks/ folder:

📜 License
This project is licensed under the MIT License.
