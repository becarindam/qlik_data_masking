Qlik Data Masking
A utility to mask Parquet files generated from Qlik Sense apps, enabling safe development and migration of Qlik Sense dashboards without compromising data privacy. The tool retains data granularity, volume, and cardinality while masking sensitive data.

🚀 Features
Consistent Key Masking: Ensures joins remain intact by applying deterministic hashing.
Dynamic Masking Techniques: Supports data shuffling, noise addition, PII anonymization, and field exclusion.
Preserve Date/Time Fields: Skips masking for DATE_TIME fields to maintain time-based analyses.
Masked and Unmasked Handling: Automatically handles excluded files by copying them as unmasked_* files.
📂 Project Structure
plaintext
Copy
Edit
qlik_data_masking/
│
├── data/
│   ├── parquet/
│   │    ├── ADVISOR.parquet                # Sample Parquet file
│   │    ├── FactTable.parquet              # Sample Fact Table
│   │    ├── exclude_this_file.parquet      # File to be excluded
│   │    ├── masked/                        # Output folder for masked files
│   │         ├── masked_ADVISOR.parquet
│   │         ├── unmasked_exclude_this_file.parquet
│   │
├── recommend_masking.py                    # Script to generate masking recommendations
├── mask.py                                 # Main masking script
├── masking_recommendations.csv             # CSV with recommended masking algorithms
├── requirements.txt                        # Python dependencies
└── README.md                               # Project documentation
🔧 Installation
Clone the repository:
bash
Copy
Edit
git clone https://github.com/YOUR_USERNAME/qlik_data_masking.git
cd qlik_data_masking
Create a virtual environment (Optional):
bash
Copy
Edit
python -m venv venv
source venv/bin/activate       # On Linux/Mac
venv\Scripts\activate          # On Windows
Install dependencies:
bash
Copy
Edit
pip install -r requirements.txt
📖 Usage
🟢 Step 1: Export Qlik Sense Data to Parquet
Load all tables from the Qlik Sense app as Parquet files.
Refer to the parquet.txt for a sample Qlik load script.
🟢 Step 2: Generate Masking Recommendations
bash
Copy
Edit
python recommend_masking.py
This will analyze your Parquet files and generate masking_recommendations.csv.
🟢 Step 3: Apply Data Masking
bash
Copy
Edit
python mask.py
The script will:
Mask the sensitive fields based on masking_recommendations.csv.
Exclude specific files and copy them as unmasked_*.parquet files.
🟢 Step 4: Verify Masked Files
The masked files are generated in the data/parquet/masked folder.
Unmasked files are prefixed with unmasked_.
🟢 Step 5: Update Qlik Sense App
Duplicate the QVF or QVW file.
Repoint data connections to the masked_*.parquet files.
Refresh the dashboard to verify the masked data.
🚨 Example: Excluding Files from Masking
To exclude a file from masking, add it to the excluded_files list in mask.py:

python
Copy
Edit
excluded_files = ['exclude_this_file.parquet']
The file will be copied as unmasked_exclude_this_file.parquet in the masked folder.

✅ Best Practices
Backup Qlik Sense apps before re-pointing to masked data.
Test the data integrity after masking, especially for key fields.
Ensure excluded files are correctly handled and not modified.
📦 Requirements
Python 3.8+
Packages:
plaintext
Copy
Edit
pandas
pyarrow
presidio-analyzer
presidio-anonymizer
faker
📄 License
This project is licensed under the MIT License. See the LICENSE file for details.
