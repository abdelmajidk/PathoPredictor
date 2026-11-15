# PathoPredictor

## Reconstructed research repository

This repository provides a **reconstructed machine-learning analysis**
associated with the published article:

**PathoPredictor: A Machine Learning Framework for Predicting
Pathogenic Missense Variants in the Human Genome**

Published article:
https://www.mdpi.com/3042-8424/1/1/3

> **Important scientific disclosure:** The original code and exact
> dataset used for the published study have not yet been recovered.
> This repository is a later reconstruction, **not an exact
> reproduction of the published experiment**.

## Differences from the published study

| Aspect | Published study | Current reconstruction |
|---|---|---|
| Variants | 59,302 | 201,225 unique variants |
| Predictors | 28 | 13 |
| ClinVar | November 2023 | Later available data |
| dbNSFP | 5.1, GRCh37 | 5.1a, GRCh37 |
| Evaluation | Five-fold cross-validation | Train/validation/held-out test |
| Classifiers | Six classifiers | Six reconstructed classifiers |
| SVM | Published configuration | Calibrated linear SVM |

The reconstructed predictor set includes
`fathmm-XF_coding_score`, which is not interchangeable with
`fathmm-MKL`.

**Do not cite reconstructed metrics as results from the original
published experiment.**

## Repository contents

- `notebooks/PathoPredictor_reproducible.ipynb` — reconstructed
  analysis notebook.
- `notebooks/PathoPredictor_reconstructed.ipynb` — fuller
  historical reconstruction and exploration.
- `data/` — derived ClinVar candidate and matched annotation CSVs.
- `models/` — saved reconstructed model and selection metadata.
- `results/tables/` — reconstructed results tables.
- `results/figures/` — reconstructed visualizations.

The large original source archives are **not included**.

## Reconstructed analysis

The available reconstruction contains 201,225 unique variants:
137,402 benign and 63,823 pathogenic, with 13 predictor scores.

It uses a stratified 80/20 train/test split, followed by a
training/validation split for classifier comparison. The selected
LightGBM model was subsequently fitted on the full training partition
and evaluated on the held-out test partition.

The existing reconstructed results report approximately:

- Accuracy: 0.93915
- Precision: 0.90937
- Recall: 0.89761
- F1: 0.90345
- ROC-AUC: 0.98224
- PR-AUC: 0.96658

These are **reconstruction results only**, not the published
five-fold cross-validation results.

## Verification status and limitations

Fresh-kernel execution has been verified through data preparation,
train/test splitting, validation preprocessing, and logistic
regression validation. Random Forest training and validation metrics
also executed successfully in a separate test.

A complete independent fresh-kernel execution of all classifiers
and reporting cells has **not yet been verified**.

An earlier exploratory notebook cell evaluated logistic regression
on the reserved test partition before the subsequent
validation-based model-selection workflow. Consequently, the test
partition should not be described as untouched throughout
development.

Additional limitations include differences in data release dates,
feature availability, variant selection, and potential overlap of
genes between training and test partitions. Predictor-score
provenance and potential upstream label leakage should also be
considered when interpreting performance.

## Reproducibility

Open `notebooks/PathoPredictor_reproducible.ipynb` in Jupyter
with the required scientific Python packages installed.

The repository includes derived input CSVs to reduce dependence
on the very large upstream source archives. Software versions
and complete execution instructions are being documented as
part of the reconstruction.

The supplied `.joblib` model should be loaded only from a
trusted copy of this repository because Python model
serialization formats can execute code when loaded.

## Data availability and provenance

The CSVs in `data/` are **derived research datasets**, not the
original dataset used in the published paper. They were
reconstructed using later ClinVar records and dbNSFP 5.1a
GRCh37 annotations.

ClinVar: https://www.ncbi.nlm.nih.gov/clinvar/

dbNSFP: https://sites.google.com/site/jpopgen/dbNSFP

Users should consult the original data providers for
licensing, attribution, release information, and source files.

## Status

This repository is being released to improve transparency and
availability of the reconstructed workflow while recovery of
the original published research materials remains unresolved.
