# dataflow-automated-cleaning-reporting
A Python automation tool for cleaning, validating, analyzing, and reporting on CSV and Excel datasets with CLI, logging, and testing.

# DataFlow: Automated Data Cleaning & Reporting System

A Python-based automation tool for cleaning, validating, analyzing, and reporting on structured CSV and Excel datasets. DataFlow provides a repeatable data-quality workflow through a command-line interface, documented cleaning rules, logging, automated reports, and testing.

## Problem

Organizations often work with datasets containing missing values, duplicate records, inconsistent formatting, invalid numeric values, and inconsistent dates. Manual cleaning is repetitive and difficult to audit.

## Solution

DataFlow automates data ingestion, validation, cleaning, quality analysis, and report generation while recording processing metrics and errors. The raw input file remains unchanged.

## Features

- CSV and Excel file ingestion
- Required-column validation
- Missing-value profiling
- Duplicate detection and removal
- Text and email normalization
- Numeric and date validation
- Cleaned CSV and Excel exports
- JSON data-quality reports
- Column-quality and summary-statistics reports
- Matplotlib visual summaries
- Structured logging
- Optional SQLite audit persistence
- Command-line interface
- Automated tests with pytest

## Tech Stack

- Python
- Pandas
- NumPy
- OpenPyXL
- Matplotlib
- SQLite
- pytest
- Git and GitHub

## Project Structure

```text
dataflow/
├── data/
│   ├── raw/
│   ├── processed/
│   └── reports/
├── docs/
├── evidence/
├── src/dataflow/
│   ├── cleaning/
│   ├── cli.py
│   ├── config.py
│   ├── database.py
│   ├── ingestion.py
│   ├── pipeline.py
│   └── reporting.py
├── tests/
├── main.py
├── requirements.txt
├── requirements-dev.txt
├── pyproject.toml
├── .gitignore
├── LICENSE
└── README.md
```

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/dataflow-automated-cleaning-reporting.git
cd dataflow-automated-cleaning-reporting
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

## Usage

Run the sample dataset:

```bash
python main.py --input data/raw/sample_customers.csv --output data/processed/
```

Run with validation and type-conversion options:

```bash
python main.py --input data/raw/sample_customers.csv --output data/processed/ --required-columns customer_id,name,email,age,signup_date --numeric-columns age,spend --date-columns signup_date
```

Run with SQLite audit persistence:

```bash
python main.py --input data/raw/sample_customers.csv --output data/processed/ --sqlite data/reports/dataflow_audit.db
```

Display help:

```bash
python main.py --help
```

## Cleaning Rules

DataFlow applies documented, conservative transformations:

- Column names are normalized to lowercase snake_case.
- Text values are stripped of surrounding whitespace.
- Email values are converted to lowercase.
- Configured numeric columns use safe numeric conversion.
- Configured date columns use safe date parsing.
- Invalid conversions are recorded as missing values.
- Exact duplicate rows are removed after normalization.
- Missing values are reported rather than silently imputed.

See `docs/CLEANING_RULES.md` for details.

## Generated Outputs

The pipeline generates:

- Cleaned CSV file
- Cleaned Excel file
- Column-quality report
- Summary-statistics report
- JSON data-quality report
- Missing-value visualization
- Processing log
- Optional SQLite audit record

## Sample Results

The included sample dataset contains intentionally imperfect records for testing the workflow. A sample run detects duplicate records, missing values, invalid numeric values, and invalid dates.

The generated reports and verification evidence can be found in the `data/processed/` and `evidence/` directories after execution.

## Testing

Run the automated tests:

```bash
pytest -q
```

Run tests with coverage:

```bash
pytest --cov=src/dataflow --cov-report=term-missing
```

## Design Decisions

### Modular architecture

The project separates ingestion, cleaning, reporting, logging, persistence, and pipeline orchestration to improve maintainability and testability.

### Conservative transformations

DataFlow does not overwrite raw input files. Cleaning rules are documented, and invalid conversions are reflected in the processing metrics.

### CLI-first workflow

The command-line interface supports repeatable execution and can be integrated into future scheduled or automated workflows.

## Limitations

- Designed for tabular CSV and Excel files.
- Business-specific validation rules must be configured explicitly.
- Exact duplicate detection is not a substitute for domain-specific duplicate identification.
- Large datasets may require chunked processing.
- The initial version does not include a web dashboard.

## Future Improvements

- YAML configuration support
- Chunked processing for large files
- Additional validation rules
- Streamlit dashboard
- Scheduled processing
- Cloud storage integration
- Data lineage tracking

## License

This project is licensed under the MIT License. See `LICENSE` for details.
