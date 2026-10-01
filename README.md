# Dataset Folder

This folder contains all raw, intermediate, and derived data files used in the analyses reported in the manuscript *"Tumor-Level Genomic Instability and Metastatic Clonal Selection in Renal Cell Carcinoma: An Interpretable Machine-Learning Analysis of Multi-Region Sequencing Data."*

## Raw source data (third-party, redistributed under original data-sharing terms)

| File | Source | Description |
|---|---|---|
| `Dryad.zip` | Naxerova et al. 2017 (*Science*) / Reiter et al. 2020 (*Nature Genetics*) | Raw phylogenetic tree data and polyguanine genotypes for the colorectal cancer discovery cohort. Original DOI: [10.5061/dryad.vv53d](https://doi.org/10.5061/dryad.vv53d). |
| `mmc1.xlsx` | Turajlic et al. 2018 (*Cell*), TRACERx Renal | Supplementary Table S1: patient-level clinical, demographic, and molecular covariates (evolutionary subtype, wGII, ITH index, stage, grade, etc.) for the TRACERx Renal cohort. |
| `mmc6.xlsx` | Turajlic et al. 2018 (*Cell*), TRACERx Renal | Supplementary Table S6: per-event mutation, driver-SCNA, and arm-level SCNA calls with primary-tumor and metastasis clonal status for each of 37 patients. This is the primary source table from which the event-level selection dataset is derived. |
| `Supplemental_Data.xlsx` | Puccini et al. 2021 (*npj Precision Oncology*) | Processed NGS gene-panel prevalence data (lymph node / distant metastasis / primary tumor) for an independent colorectal cancer cohort, used in the cross-cancer-type comparison. Original source: [figshare doi:10.6084/m9.figshare.14854383](https://doi.org/10.6084/m9.figshare.14854383). |

## Derived data (produced by this study's analysis pipeline)

| File | Produced by | Description |
|---|---|---|
| `events_merged_full.csv` | `Build_Selection_Dataset.ipynb` | Full merged event-level dataset (2,177 rows): every mutation/SCNA event from `mmc6.xlsx`, standardized into a common schema, labeled with its selection category (`selected`, `not_selected`, `retained_subclonal`, `already_clonal`, `de_novo_in_met`), and merged with patient-level covariates from `mmc1.xlsx`. |
| `binary_selection_dataset.csv` | `Build_Selection_Dataset.ipynb` | The 1,195-row subset of `events_merged_full.csv` restricted to the binary classification task (`selected` vs. `not_selected`), used as the primary input for all downstream modeling, robustness, and locus-enrichment notebooks. |
| `Supplementary_Tables.xlsx` | All analysis notebooks (compiled) | The complete Supplementary Tables S1-S5 referenced throughout the manuscript as "Additional file 1": RDS pipeline validation (S1), full event-level dataset (S2), model performance comparison (S3), systematic locus-enrichment screen (S4), and cross-cancer-type gene comparison (S5). |

## Reproducing the pipeline from scratch

Running the notebooks in this order regenerates every derived file above:

1. `RDS_Pipeline.ipynb` — validates the Root Diversity Score implementation against `Dryad.zip`
2. `Build_Selection_Dataset.ipynb` — produces `events_merged_full.csv` and `binary_selection_dataset.csv` from `mmc1.xlsx` and `mmc6.xlsx`
3. `Classifier_SHAP_Analysis.ipynb`, `Robustness_Checks.ipynb`, `Locus_Enrichment_Validation.ipynb` — consume `binary_selection_dataset.csv`
4. `Cross_Cancer_Comparison.ipynb` — consumes `binary_selection_dataset.csv` and `Supplemental_Data.xlsx`

See the repository root `README.md` for environment setup (`requirements.txt`) and full notebook descriptions.
