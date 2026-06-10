# time_series_forecasting

Course materials for time series forecasting: data exploration, ARIMA modeling, and AutoML with AutoGluon, using energy and production datasets. The goal is to provide hands-on practice with real-world time series data across the full forecasting workflow — from pattern discovery to automated model selection.

## What's in this repo

| File                                    | What it does                                                                      |
| --------------------------------------- | --------------------------------------------------------------------------------- |
| `class_1_data_aggregation.ipynb`        | Data aggregation techniques for time series analysis.                             |
| `class_2_time_patterns.ipynb`           | Identifying and analyzing temporal patterns.                                      |
| `class_3_acf_pacf.ipynb`               | Autocorrelation and partial autocorrelation functions.                            |
| `4_ARIMA.ipynb`                         | ARIMA model: stationarity, ACF/PACF, model fitting and forecasting.               |
| `5_AutoGluon.ipynb`                     | AutoML time series forecasting with AutoGluon.                                    |
| `smart_meter_data.csv`                  | Half-hourly electricity consumption from smart meters.                            |
| `UK_electricity_demand_2024.csv`        | UK electricity demand for the year 2024.                                          |
| `AUS quaterly beer production.csv`      | Quarterly beer production in Australia (1956–2010).                               |
| `AUS monthly beer production.csv`       | Monthly beer production in Australia (1956–2010).                                 |
| `requirements.txt`                      | Pinned list of all Python dependencies.                                           |
| `pyproject.toml`                        | Declares dependencies and Python version (`==3.13.*`).                            |
| `.gitignore`                            | Excludes `.venv/` and `__pycache__/` from git.                                    |

## One-time: install uv

macOS / Linux:

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows (PowerShell):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Source of truth: https://docs.astral.sh/uv/getting-started/installation/

## How to run this project

```sh
git clone https://github.com/francescaconselvan/time_series_forecasting.git
cd time_series_forecasting
uv sync          # creates .venv/, downloads Python 3.13 if needed, installs deps from uv.lock
## >> Activate the virtualenv in .venv (created in the previous command)
jupyter notebook
```

Then open any of the `.ipynb` notebooks from the Jupyter interface in your browser.


## Cheat sheet for pip / conda users

| Task                  | pip / conda                                                             | uv                                                           |
| --------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------ |
| Create environment    | `python -m venv .venv` / `conda create -n x python=3.11.9`               | `uv sync` (reads `.python-version`)                          |
| Install a package     | `pip install autogluon`                                                 | `uv add autogluon`                                           |
| Install from lockfile | `pip install -r requirements.txt`                                       | `uv sync`                                                    |
| Freeze dependencies   | `pip freeze > requirements.txt`                                         | `uv lock` (cross-platform + hashed, updates automatically)   |
| Launch notebooks      | `source .venv/bin/activate && jupyter notebook`                         | `source .venv/bin/activate && jupyter notebook` (same)       |

Mental model: `pyproject.toml` ≈ `requirements.txt` (what you want),
`uv.lock` ≈ `pip freeze` output (what you resolved to — but cross-platform
and hashed). Commit both.

## Resources

### Books
- Hyndman & Athanasopoulos — *Forecasting: Principles and Practice* (OTexts, 2018)
  [Free online](https://otexts.com/fpp3/) — introduction to preprocessing and forecasting models; examples in R.
- Nielsen — *Practical Time Series Analysis* (O'Reilly, 2019)
  Practical guide covering data engineering, statistical, and ML techniques in both R and Python.
- Nield — *Essential Math for Data Science* (O'Reilly, 2022)

### Datasets

Accessing built-in datasets in Python via `statsmodels`:

```python
import statsmodels.api as sm
# sunspots, co2, nile, macrodata, elnino
```

Access R datasets from Python:

```python
from statsmodels.datasets import get_rdataset
```

External sources:
- [UCI Machine Learning Repository](https://archive.ics.uci.edu/) — time series datasets
- [NOAA National Centers for Environmental Information](https://perma.cc/EA5R-TP5L) — US temperature and precipitation time series

### Learning links
- [StatQuest](https://www.youtube.com/@statquest) — statistics tutorials

## License

Course materials for educational purposes.
