# Predicting Student Test Scores

This repository contains a Jupyter notebook that builds a machine learning pipeline to predict student exam scores using the dataset in the `data/` folder.

## Files
- `main.ipynb` — end-to-end notebook: EDA, feature engineering, K-Fold safe target encoding, LightGBM training (5-fold CV), and submission generation.
- `data/train.csv`, `data/test.csv`, `data/sample_submission.csv` — dataset files (committed to the repo).
- `submission.csv` — example output produced by the notebook.

## Quick start
1. Create (or activate) a Python environment with the required packages.

Recommended minimal install:

```powershell
pip install -r requirements.txt
```

If you don't have `requirements.txt`, install these packages:

```powershell
pip install pandas numpy scikit-learn lightgbm xgboost catboost matplotlib seaborn
```

2. Open the notebook: `main.ipynb` and run cells in order. The notebook reads data from the `data/` folder and writes `submission.csv` to the repo root.

3. Notes:
- The notebook implements K-Fold out-of-fold target encoding to avoid target leakage; raw categorical columns are dropped after encoding.
- For reproducible LightGBM runs, fix `random_state`, `n_jobs=1`, and set LightGBM seeds if deterministic behavior is required.
- The `data/` files are included here for convenience. If you prefer not to track them with git, revert the `.gitignore` entry.

## Contact
If you want changes (add experiments, CI, or scripts for training), tell me and I can add them.
