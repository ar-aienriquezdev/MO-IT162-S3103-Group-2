# FinMarks — Milestone 2: Data Visualization (Draft)

This milestone delivers a reproducible workflow for:
- cleaning + merging the input datasets, and  
- producing exploratory data visualizations **with statistical notes printed above each chart** (ANOVA, Pearson correlations, Chi-square tests) plus an **ADF stationarity test** for the time-series view.

> ✅ No user-specific paths are hardcoded. The notebooks work on macOS, Windows, and Linux.

---

## Repo Structure (Milestone 2)

```
.
├─ FinMarks_Dataset_Preprocessing_Robust_Generic.ipynb     # load/clean/merge → merged_cleaned_dataset.csv
├─ FinMarks_Datasets_EDA-Data_Visualization_clean_ADF_v5.ipynb  # visuals + text notes + ADF + auto chi-square
├─ data/                              # (optional) place raw CSVs here
├─ eda_outputs/                       # figures & tables exported by the EDA notebook (created on run)
└─ merged_cleaned_dataset.csv         # created by preprocessing notebook
```

**Input CSVs expected:**
- `customer_demographics_contaminated.csv`
- `customer_transactions_contaminated.csv`
- `social_media_interactions_contaminated.csv`

---

## Quick Start

### 1) Clone

```bash
git clone <YOUR-REPO-URL>.git
cd <YOUR-REPO-NAME>
```

### 2) Create & activate an environment (choose one)

**Python venv**
```bash
python -m venv .venv
# macOS/Linux
source .venv/bin/activate
# Windows (PowerShell)
.venv\Scripts\Activate.ps1
```

**OR Conda**
```bash
conda create -n finmarks-eda python=3.10 -y
conda activate finmarks-eda
```

### 3) Install dependencies

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
```

> Minimum versions: Python 3.9+.

---

## Data Placement (robust path resolution)

The preprocessing notebook searches for the input CSVs in this order:

1. Directory pointed to by environment variable `RAW_DIR` (optional)  
2. Current directory  
3. Parent directory  
4. `./data`  
5. Home directory  
6. Home `Downloads`

If not found directly, it does a **bounded recursive search** under those locations.

**Option A — put the files next to the notebooks**  
Just drop the three CSVs beside the notebooks.

**Option B — use a data folder**
```
mkdir -p data
# place CSVs here
```

**Option C — point to a custom path via env var**
```bash
# macOS/Linux
export RAW_DIR=~/my_data_folder
# Windows (PowerShell)
$env:RAW_DIR="C:\my_data_folder"
```

---

## Run Order

### 1) Preprocessing
Open and run all cells in:
```
FinMarks_Dataset_Preprocessing_Robust_Generic.ipynb
```
Outputs:
- `merged_cleaned_dataset.csv` (root of repo)
- Console logs: resolved file paths, merged shape, unique customer count

### 2) EDA & Visualizations
Open and run all cells in:
```
FinMarks_Datasets_EDA-Data_Visualization_clean_ADF_v5.ipynb
```

What it produces:
- **Histograms, bar charts, box plots, correlation heatmap**
- **Text notes printed above plots** for:
  - ANOVA (e.g., `total_spent ~ gender`)
  - Pairwise **Pearson correlation significance report** (text-only, r & p for all numeric pairs)
  - **Chi-Square** tests for categorical pairs (auto-detected; prints ranked summary and shows charts for top results)
- **Time series** of monthly `total_spent` with **ADF** stationarity test (statistic, p-value, interpretation)
- Exports PNGs/CSVs (where applicable) into `eda_outputs/`

---

## Troubleshooting

- **Notebooks won’t edit or run in VS Code**
  - Switch from “Preview” to the **Notebook** editor.
  - Make sure the file isn’t read-only (`chmod u+w <file>.ipynb` on macOS/Linux).
  - Command Palette → **“Trust Notebook”**.
- **CSV not found**
  - Confirm filenames match exactly.
  - Move the files beside the notebooks, into `./data`, or set `RAW_DIR` (see above).
- **Missing package**
  - `pip install <package>` (e.g., `pip install statsmodels`).

---

## Milestone 2 Summary (what to expect)

- **Clean, merged dataset** ready for modeling: `merged_cleaned_dataset.csv`
- **Visual narratives** with statistical context displayed before each figure:
  - ANOVA results and interpretations
  - Pearson correlation r & p across all numeric pairs
  - Chi-Square tests for categorical associations (top pairs)
  - ADF test for trend stationarity + monthly plot
- **Portable & reproducible** notebooks (no personal paths; OS-agnostic resolution)

---

## Next Steps (beyond Milestone 2)

- Add narrative markdown around the most relevant insights.
- Tie selected features/insights to candidate modeling approaches for Milestone 3.
