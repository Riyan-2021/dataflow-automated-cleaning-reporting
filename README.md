# DataFlow: Automated Data Cleaning & Reporting System

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Tests](https://img.shields.io/badge/tests-pytest-green.svg)](https://pytest.org/)
[![License](https://img.shields.io/badge/license-MIT-lightgrey.svg)](LICENSE)

DataFlow is a modular Python command-line application that ingests CSV and Excel files, validates data quality, applies documented cleaning rules, generates analytical summaries, exports cleaned data, and records processing activity through structured logs.

## Problem

Organizations often receive structured datasets containing missing values, duplicate rows, inconsistent text formats, invalid numeric values, and inconsistent date formats. Cleaning these files manually is repetitive, difficult to audit, and prone to inconsistent decisions.

## Solution

DataFlow provides a repeatable workflow:

1. Ingest CSV or Excel files.
2. Validate required columns and common quality issues.
3. Apply documented cleaning rules.
4. Calculate data-quality metrics and summary statistics.
5. Export cleaned data and machine-readable reports.
6. Record processing steps and errors in a log file.

## Features

- CSV and Excel input support
- Required-column validation
- Missing-value profiling
- Duplicate detection and removal
- Text normalization
- Numeric coercion with invalid-value tracking
- Date parsing with invalid-date tracking
- Configurable missing-value handling
- CSV and Excel cleaned-data output
- JSON data-quality report
- CSV column-quality report
- Summary statistics report
- Matplotlib visual summary
- SQLite audit persistence
- Command-line interface
- Structured logging
- Automated tests with pytest
- Sample dataset and reproducible evidence

## Technology Stack

- Python 3.10+
- Pandas
- NumPy
- OpenPyXL
- Matplotlib
- SQLite
- pytest
- Git/GitHub

## Project Structure

```text
dataflow/
├── data/
│   ├── raw/
│   │   └── sample_customers.csv
│   ├── processed/
│   └── reports/
├── docs/
│   ├── DATA_DICTIONARY.md
│   ├── CLEANING_RULES.md
│   └── EVIDENCE.md
├── evidence/
│   ├── sample_run_summary.md
│   └── screenshots/
├── src/
│   └── dataflow/
│       ├── __init__.py
│       ├── cli.py
│       ├── config.py
│       ├── database.py
│       ├── ingestion.py
│       ├── logging_config.py
│       ├── pipeline.py
│       ├── reporting.py
│       └── cleaning/
│           ├── __init__.py
│           ├── rules.py
│           └── service.py
├── tests/
│   ├── test_cleaning.py
│   ├── test_ingestion.py
│   └── test_reporting.py
├── main.py
├── pyproject.toml
├── requirements.txt
├── requirements-dev.txt
├── .gitignore
├── LICENSE
└── README.md
```

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/dataflow.git
cd dataflow
```

### 2. Create and activate a virtual environment

Windows PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

Windows Command Prompt:

```cmd
python -m venv .venv
.venv\Scripts\activate
```

macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

## Usage

Run the sample CSV file:

```bash
python main.py --input data/raw/sample_customers.csv --output data/processed/
```

Run with a custom required-column list:

```bash
python main.py \
  --input data/raw/sample_customers.csv \
  --output data/processed/ \
  --required-columns customer_id,name,email,age,signup_date
```

Run with SQLite audit persistence:

```bash
python main.py \
  --input data/raw/sample_customers.csv \
  --output data/processed/ \
  --sqlite data/reports/dataflow_audit.db
```

Show CLI help:

```bash
python main.py --help
```

## Output Files

A successful run produces:

```text
data/processed/
├── cleaned_sample_customers.csv
├── cleaned_sample_customers.xlsx
├── column_quality_sample_customers.csv
├── summary_statistics_sample_customers.csv
├── data_quality_report_sample_customers.json
├── quality_summary_sample_customers.png
└── dataflow.log
```

The exact output names are generated from the input filename.

## Cleaning Rules

The default rules are intentionally conservative and documented in `docs/CLEANING_RULES.md`.

Examples:

- Column names are normalized to lowercase snake_case.
- Text values are stripped of leading/trailing whitespace.
- Email values are lowercased.
- Numeric columns are converted using safe coercion.
- Invalid numeric values become missing and are recorded.
- Dates are parsed using safe coercion.
- Duplicate rows are removed using all available columns.
- Missing values are reported; numeric missing values are not automatically imputed unless explicitly configured.

## Testing

Run the test suite:

```bash
pytest -q
```

Run with coverage if `pytest-cov` is installed:

```bash
pytest --cov=src/dataflow --cov-report=term-missing
```

## Sample Results

The repository includes a deliberately imperfect sample dataset. It contains duplicate rows, missing values, inconsistent casing, whitespace, invalid numeric data, and an invalid date.

After processing, DataFlow produces:

- Cleaned CSV and Excel files
- Column-level quality metrics
- Summary statistics
- A JSON quality report
- A visual quality summary
- A processing log
- Optional SQLite audit records

See `evidence/sample_run_summary.md` for a reproducible sample-run record.

## Design Decisions

### Why a CLI?

A command-line interface makes the workflow reusable in scripts, scheduled jobs, CI pipelines, and future web interfaces.

### Why modular architecture?

Separating ingestion, cleaning, reporting, persistence, and orchestration makes the project easier to test, extend, and maintain.

### Why preserve evidence?

Data cleaning is a transformation. A professional workflow should expose the rules, counts, warnings, and outputs rather than silently changing the source data.

## Limitations

- The current version is designed for tabular CSV and Excel data.
- It does not automatically infer business-specific validation rules.
- The default duplicate rule uses all columns; domain-specific keys can be added later.
- Very large datasets may require chunked processing.
- No web dashboard is included in the first version.

## Future Improvements

- YAML-based configuration
- Chunked processing for large files
- Data profiling with richer statistical diagnostics
- Great Expectations or Pandera integration
- Scheduled execution
- Streamlit dashboard
- Cloud storage support
- Data lineage tracking
- User-defined validation rules

## License

This project is released under the MIT License. See `LICENSE`.
