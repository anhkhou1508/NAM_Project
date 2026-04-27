# NAM Project — Interpretable 30-day Hospital Readmission Prediction

Honours-project codebase. Implements interpretable readmission prediction on the
**UCI Diabetes 130-US Hospitals** dataset using **DNAMite**-based Neural Additive
Models, compared against a logistic-regression baseline.

The notebook in this repository is committed **with all cell outputs rendered**
(figures, classification reports, ROC curves, feature importances, shape
functions). You can browse the results directly on GitHub or in any local
Jupyter viewer without re-running anything.

---

## Repository contents

| Path | Purpose |
|---|---|
| `2540640_NAM.ipynb` | Main notebook with all experiments and rendered outputs. |
| `diabetic_data.csv` | UCI Diabetes 130-US Hospitals dataset used by the notebook. |
| `requirements.txt` | Pinned Python dependencies used to produce the rendered outputs. |
| `README.md` | This file. |

The dataset file `diabetic_data.csv` is included in the repository so the
notebook can be re-run end-to-end without any additional downloads. The original
source is documented under *Data setup* below for reference.

---

## Quick start (read-only)

If you just want to inspect the results, open
`2540640_NAM.ipynb` directly on GitHub or in VS Code / JupyterLab. All
figures, tables and classification reports are pre-rendered.

---

## Reproducing the experiments

### 1. Environment

Tested with Python 3.11 on macOS / Linux.

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
python -m ipykernel install --user --name nam-project --display-name "NAM Project"
```

### 2. Data setup

The UCI Diabetes 130-US Hospitals dataset (`diabetic_data.csv`) is bundled in
the repository root, so no additional download is required. For reference, the
original source is:

- Source: <https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008>
- Direct ZIP: <https://archive.ics.uci.edu/static/public/296/diabetes+130+us+hospitals+for+years+1999+2008.zip>

Expected layout:

```
NAM_Project/
├── 2540640_NAM.ipynb
├── diabetic_data.csv
├── requirements.txt
└── README.md
```

### 3. Run the notebook

Open `2540640_NAM.ipynb` in JupyterLab or VS Code, select the
`NAM Project` kernel, and execute cells top-to-bottom.

The notebook is organised into five experimental phases:

1. **Data preprocessing** — replicates Strack et al. (2014) with leakage-free
   target encoding.
2. **Logistic-regression feature scouting** — identifies the *Gold 10* features
   by Z-score on an unweighted GLM.
3. **DNAMite hyperparameter tuning** — four-stage GridSearch.
4. **NAM evaluation with class-balancing strategies** — no balancing,
   Random Oversampling, SMOTE-NC.
5. **DNAMite Lasso-gated feature selection** — three-stage regularisation
   sweep, retraining on the 10/20/35-feature subsets retained at three
   regularisation levels.

End-to-end runtime is approximately 30–60 minutes on a CPU, depending on the
machine. No GPU is required.

---

## Reference

Strack, B., DeShazo, J. P., Gennings, C., Olmo, J. L., Ventura, S.,
Cios, K. J., & Clore, J. N. (2014). *Impact of HbA1c Measurement on Hospital
Readmission Rates: Analysis of 70,000 Clinical Database Patient Records.*
BioMed Research International, 2014, 781670.
