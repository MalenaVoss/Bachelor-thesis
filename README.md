# Bachelor-thesis

## ANALYSIS OF BLOOD AND URINE PROTEOMES ACROSS COLORECTAL CANCER STAGES

This repository contains the code used for the statistical analysis of the proteomic data from the VICTORIA trial.

The VICTORIA trial contained proteomic serum and urine data and was analysed to explore whether vitamin D supplementation has an effect on the proteome. In this thesis the main focus was the combination of CRC cancer stage and vitamin D supplementation, to explore whether the proteomic response to vitamin D supplementation differs depending on CRC stage.

## Hypotheses

1. Vitamin D3 supplementation induces differential protein expression compared to placebo.
2. The effect of vitamin D3 supplementation on protein expression is modulated by CRC stage (treatment × stage interaction).

Both hypotheses were tested in serum and urine. The main analysis tests treatment alone and the CRC stage × treatment interaction, not CRC stage alone.

## Data processing pipeline

- Raw proteomics data processed via a DIA-PASEF pipeline (FragPipe / MSFragger / DIA-NN)
- Missing value filtering at a 70% NA threshold
- KNN imputation of remaining missing values
- Batch correction using PyComBat

## Statistical methods

| Test | Purpose |
|---|---|
| **PERMANOVA** (overall and pairwise) | Testing group-level differences in overall proteomic composition; pairwise comparisons corrected for multiple testing using Benjamini-Hochberg FDR (via `PyPerMANOVA`) |
| **Kruskal-Wallis** | Non-parametric test for differences across more than two groups |
| **Mann-Whitney U** | Non-parametric pairwise group comparison; preferred over the t-test due to non-normality of the data |
| **Longitudinal within-arm Kruskal-Wallis** | Testing changes over time within each treatment arm |
| **Wilcoxon signed-rank** | Identified as the appropriate paired test for repeated-measures comparisons |

Additional technical notes:

- Multiple testing correction: Benjamini-Hochberg (BH) FDR correction applied as standard throughout
- Distance metric: Euclidean distance on log2-transformed data
- Effect size / significance thresholds: fold-change threshold of 0.58 (log2), FDR-adjusted p-values reported alongside effect sizes
- Differential expression results visualized as volcano plots (log2 fold-change on the x-axis, -log10(p_adj) on the y-axis)
- Ordination visualized using PCA
- Functional enrichment analysis performed using gProfiler

## Key findings

- CRC stage, rather than vitamin D allocation, was the dominant driver of proteomic variance
- Two proteins, P05546 (Heparin Cofactor II) and Q14624 (ITIH4), were significantly upregulated in the VitaminD_early group of the serum data
- Urine proteome was only significant based on allocation not allocation and cancer stage
- Discordance between serum and urine results is discussed as biologically expected rather than as a limitation
