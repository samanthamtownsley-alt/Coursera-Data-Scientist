# IBM Data Analyst Capstone — Lab Notebooks

Completed Jupyter notebooks from the IBM Skills Network Data Analyst Capstone track (course code DA0321EN). The labs move through the full analysis pipeline: data collection (APIs and web scraping), data wrangling, exploratory data analysis, and visualization.

Most labs operate on a Stack Overflow Developer Survey extract hosted by IBM Skills Network; the collection labs use a Flask-served jobs dataset and two static HTML pages.

## Contents

### 1. Data Collection

| Notebook | Description |
|---|---|
| `Review_Of_Accessing_APIs_requesting_HTP.ipynb` | HTTP fundamentals — URLs, request/response objects, headers, status codes, GET with URL parameters, POST requests, downloading files with `requests`. |
| `Jobs_API.ipynb` | Flask server implementation of the Jobs API. Loads `jobs.json` and exposes `/`, `/data/all`, and `/data` with filtering by Job Title, Key Skills, Location, Role, and other keys. Must be running before the client lab below. |
| `Collecting_job_data_using_APIs-Lab.ipynb` | Client lab. Calls the Jobs API to count job postings by technology and location, then writes results to an Excel workbook via `openpyxl`. |
| `Web-Scraping-Review-Lab.ipynb` | BeautifulSoup walkthrough — download a page, scrape all `<a>` links and `<img>` sources from ibm.com, and parse an HTML color-code table. |
| `Web-Scraping-Lab.ipynb` | Scrape programming language names and average annual salaries from a static HTML table and write to `popular-languages.csv`. |

### 2. Data Wrangling

| Notebook | Description |
|---|---|
| `M1ExploreDataSet-lab_V2.ipynb` | Initial dataset exploration — shape, column dtypes, summary statistics, unique value counts. |
| `Hands-on_Lab_Finding_Duplicates_v2.ipynb` | Identify duplicate rows, analyze duplicate response patterns, visualize duplicate distribution by key attributes. |
| `Hands-on_Lab_7_Removing_Duplicates_v2.ipynb` | Remove duplicates with `drop_duplicates()` and verify removal. |
| `Hands-on_Lab_8_Finding_Missing_Values.ipynb` | Quantify missing values per column, visualize with a seaborn heatmap, identify majority values for imputation. |
| `Hands-on_Lab_9_Imput_Missing_Values.ipynb` | Impute missing values across columns and verify the result. |
| `Hands-on_Lab_10_Normalizing_Data.ipynb` | Min-max and other normalization applied to `ConvertedCompYearly`, with before/after distribution plots. |
| `M2DataWrangling-lab-v2.ipynb` | Standardize inconsistent categorical entries, one-hot encode `Employment`, multiple imputation strategies, feature scaling and transformation. |

### 3. Exploratory Data Analysis

| Notebook | Description |
|---|---|
| `Hands-on_Lab_Exploratory_Data_Analysis.ipynb` | Employment status, job satisfaction, language usage, and remote work trends; `YearsCodePro` binned against median `JobSat`. |
| `Lab_11_Finding_How_The_Data_is_Distributed.ipynb` | Distribution analysis of key columns and developer tooling/experience trends. |
| `Lab_12_Finding_Outliers.ipynb` | Outlier detection on `ConvertedCompYearly` using standard deviation thresholds and the IQR method; box plots and a cleaned DataFrame. |
| `Lab_13_Finding_Correlation.ipynb` | Compensation distribution by country, outlier removal, and correlation analysis across features. |

### 4. Data Visualization

| Notebook | Description |
|---|---|
| `Lab_Data_Visualization__1_.ipynb` | Loads the survey CSV into a SQLite database, queries it with `sqlite3`, and plots distributions, relationships, composition, and comparisons. |
| `Lab_14_Data_Visualization_-_Histogram__1_.ipynb` | Works against a provided SQLite database. Histograms of `CompTotal` and `YearsCodePro`, comparisons by `Age` group, and `TimeSearching` distributions. |

## Data Sources

All datasets are downloaded at runtime by the notebooks; none are committed to this repository.

| Source | Used by |
|---|---|
| `survey-data.csv` (Stack Overflow Developer Survey extract) | Most wrangling, EDA, and visualization labs |
| `survey-data-with-duplicate.csv` | `M1ExploreDataSet-lab_V2`, `Hands-on_Lab_Finding_Duplicates_v2` |
| `survey-results-public.sqlite` | `Lab_14_Data_Visualization_-_Histogram__1_` |
| `jobs.json` | `Jobs_API`, `Collecting_job_data_using_APIs-Lab` |
| `Programming_Languages.html` | `Web-Scraping-Lab` |
| `HTMLColorCodes.html` | `Web-Scraping-Review-Lab` |
| `httpbin.org`, `ibm.com`, `api.open-notify.org` | HTTP and scraping review labs |

## Requirements

Python 3.8+ and Jupyter. Package dependencies across all notebooks:

```
pandas
numpy
matplotlib
seaborn
requests
beautifulsoup4
openpyxl
flask
pillow
```

`sqlite3` and `json` are part of the standard library.

```bash
python -m venv .venv
source .venv/bin/activate
pip install pandas numpy matplotlib seaborn requests beautifulsoup4 openpyxl flask pillow jupyterlab
jupyter lab
```

The notebooks contain inline `!pip install` cells left over from the JupyterLite environment. They are harmless but redundant if the environment is already provisioned.

## Running the API Labs

`Collecting_job_data_using_APIs-Lab.ipynb` depends on a live server:

1. Run all cells in `Jobs_API.ipynb`. It downloads `jobs.json` and starts Flask on `http://127.0.0.1:5000` (the final `app.run()` cell blocks).
2. In a separate kernel, run `Collecting_job_data_using_APIs-Lab.ipynb` against that base URL.

Both notebooks must resolve `jobs.json` from the same working directory.

## Notes

- Several notebooks were authored for JupyterLite and include a `pyfetch`-based download helper as an alternative to reading the source URL directly with `pandas.read_csv()`. Either path works locally.
- Cell execution counts are non-sequential in some notebooks, reflecting the order in which cells were run during the labs.

## License

The original lab notebooks are Copyright © IBM Corporation and released under the [MIT License](https://cognitiveclass.ai/mit-license/). The `jobs.json` dataset derives from the [Jobs on Naukri.com](https://www.kaggle.com/promptcloud/jobs-on-naukricom) Kaggle dataset, published under a Public Domain license.
