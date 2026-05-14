# Healthcare Anesthesia Data Prep

## Virtual Environment

The project has a local virtual environment at:

```bash
.venv
```

It was created with system site packages so it can use the available pandas install without downloading packages:

```bash
python3 -m venv --system-site-packages .venv
```

Notebook/runtime libraries are listed in:

```bash
requirements.txt
```

Install or refresh them with:

```bash
.venv/bin/python -m pip install -r requirements.txt
```

Run the Python script with:

```bash
.venv/bin/python scripts/prepare_anesthesia_claims.py
```

## Notebook

Open this notebook in VS Code or Jupyter:

```bash
notebooks/anesthesia_data_prep.ipynb
```

When prompted for a kernel/interpreter, choose:

```bash
.venv/bin/python
```

The notebook shows the step-by-step outputs for loading, filtering, merging, validation counts, preview rows, and saving the final CSV.

It also includes Key Business Question 1 analysis:

- 100% stacked bar charts for yearly product share by claims, patients, and HCP writers
- Line charts for claims per writer and patients per writer
- Top 5 Product 2 drop territories from 2017 to 2018
- Product 2 versus Product 3 clustered bar comparison for those territories
- Observations and actionable recommendations

## Final Output

```bash
outputs/analysis_ready_claims_python.csv
```
