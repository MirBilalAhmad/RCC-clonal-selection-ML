# RCC-clonal-selection-ML
This repository contains the complete analysis code accompanying the manuscript "Tumor-Level Genomic Instability and Metastatic Clonal Selection
in Renal Cell Carcinoma: An Interpretable Machine-Learning Analysis of Multi-Region Sequencing Data." It includes: 

(1) an independently validated computational pipeline reproducing the Root Diversity Score (RDS) framework of Reiter et al. (2020) from raw phylogenetic tree data

(2) construction of an event-level dataset of clonal selection into metastasis from the TRACERx Renal cohort (Turajlic et al. 2018) 

(3) interpretable classifiers (random forest, logistic regression) trained under leave-one-patient-out cross-validation with SHAP-based feature attribution and bootstrap confidence intervals 

(4) a systematic, FDR-corrected locus-enrichment screen

(5) a cross-cancer-type comparison against an independent colorectal cancer cohort (Puccini et al. 2021). All analyses are provided as executed Jupyter notebooks for full reproducibility
