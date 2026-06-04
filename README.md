# petroineos-pwer-plants-challange
# Power Plants Data Pipeline

This repository contains my solution for the Power Plants data processing task. The assignment required building a self-contained Jupyter notebook to analyse, clean, load, and aggregate power plant volume data from multiple CSV files.

## Project Overview

The task involves processing three input plant datasets:

* `wind_plants.csv`
* `gas_plants.csv`
* `gas_fr_plants.csv`

The goal is to load these files sequentially into a database-style CSV file called `database.csv`, after checking and handling data quality issues such as missing values, invalid entries, duplicates, negative values, and outliers.

The solution is implemented in a single Jupyter notebook:

* `power_plants_challange.ipynb`

## Main Features

The notebook implements a `PowerPlants` class with the following functionality:

* Analyse and clean raw plant CSV files
* Handle missing, invalid, negative, and duplicate values
* Convert country codes into full country names
* Add metadata columns such as `updatedby` and `updatetime`
* Save cleaned data into `database.csv`
* Retrieve the most recently updated record for each plant and date
* Aggregate plant data into quarterly summaries
* Aggregate total power production by country and technology type
* Log important data quality issues for traceability

## Data Cleaning Approach

The pipeline addresses the identified data quality issues by:

* Dropping fully empty rows
* Replacing missing, invalid string-based, and negative `Volume` values with `0`
* Standardising column names and text values
* Mapping country codes such as `GB` and `FR` to full country names
* Detecting extreme outliers in the wind dataset
* Logging outliers in a separate logs CSV file instead of adding them to the final database

The outliers were excluded from `database.csv` because their values were significantly larger than the normal volume range in the wind dataset and would have distorted the quarterly and country-level aggregation results. They are still recorded in the logs file for transparency and traceability.

## Repository Structure

```text
.
├── power_plants_challange.ipynb   # Main notebook containing the full solution
├── wind_plants.csv                # Wind plant input data
├── gas_plants.csv                 # Gas plant input data
├── gas_fr_plants.csv              # French gas plant input data
├── database.csv                   # Generated cleaned database file
├── logs.csv                       # Generated data quality log file
└── README.md                      # Project documentation
```

## How to Run

1. Clone or download this repository.
2. Open `power_plants_challange.ipynb` in Jupyter Notebook or JupyterLab.
3. Ensure the three input CSV files are in the same directory as the notebook.
4. Run the notebook from top to bottom.

The notebook will:

1. Analyse and clean each input file.
2. Save the cleaned records into `database.csv`.
3. Generate the latest plant-level dataset.
4. Produce quarterly plant-level aggregations.
5. Produce country-level technology aggregations.
6. Save logs of important cleaning decisions and detected issues.

## Requirements

The task only requires the following Python library:

```bash
pip install pandas
```

The notebook uses standard Python libraries along with `pandas`.

## Outputs

The notebook produces three main outputs:

### 1. Cleaned Database

`database.csv` contains the cleaned and processed plant data, including metadata columns:

* `updatedby`
* `updatetime`

### 2. Latest Plant Data

The `get_data_from_database()` method returns the most recently updated record for each plant and date.

### 3. Aggregated Results

The notebook provides:

* Quarterly plant-level aggregation using mean, median, and standard deviation
* Country-level total production grouped by country and technology

## Notes

This solution is fully contained within the Jupyter notebook, as required by the task. No separate Python files are needed.
