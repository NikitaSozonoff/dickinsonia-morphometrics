# Morphometric analysis of *Dickinsonia*

This repository contains the R workflow used for a quantitative comparison of *Dickinsonia* specimens from the Middle Urals and published Australian material. The analysis was designed to test whether combinations of measurable morphological traits support the distinction of the newly described species *Dickinsonia densa* Sozonov et al., 2026.

The statistical analysis provided one line of evidence. Taxonomic interpretation also relied on comparative morphology and formal description by the full author team.

## Research context

Many species have been proposed within *Dickinsonia*. Both taxonomic inflation and excessive lumping are possible when decisions rely mainly on visual similarity. This workflow combines reproducible morphometric measurements with dimensionality reduction and model-based clustering.

## Analysis workflow

1. Read an Excel table and identify numeric variables.
2. Remove missing observations for the selected variables.
3. Optionally log-transform positive measurements.
4. Standardize variables and run principal component analysis (PCA).
5. Select the number of PCs required to explain a chosen share of variance.
6. Compare Gaussian mixture models with one to five components using `mclust` and BIC.
7. Visualize loadings, cluster assignments, provenance and specimen labels.

PCA summarizes correlated measurements as a smaller set of axes. Model-based clustering then tests probabilistic grouping structures without supplying taxonomic labels in advance. The resulting groups were interpreted together with diagnostic morphology rather than treated as automatic species assignments.

## Repository structure

```text
R/ClusterAnalysis_forPublishing.R  interactive analysis workflow
figures/                           example outputs from the analysis
```

The original specimen-level measurements are not included in this public repository.

## Input format

The script expects an Excel workbook named `Dickinsonia2024.xlsx` in the repository root. The table should contain:

- non-numeric metadata columns first;
- a `Specimen` column used for labels;
- a `Place` column used to distinguish material provenance;
- numeric morphometric variables after the metadata columns.

The script interactively asks how many numeric variables to include, whether to apply a logarithmic transformation, what cumulative variance to retain in PCA, and which of the highest-ranked mixture models to visualize.

## Requirements

Install R and the following packages:

```r
install.packages(c(
  "stringr", "dplyr", "readxl", "tidyr",
  "ggplot2", "mclust", "plotly"
))
```

Run the analysis from the repository root:

```powershell
Rscript R/ClusterAnalysis_forPublishing.R
```

Because the workflow is interactive, running it in RStudio or an R terminal is usually more convenient than a non-interactive job.

## Related publication

Sozonov et al. (2026). “The iconic Ediacaran fossil *Dickinsonia* from the Central Urals.” DOI: [10.1002/spp2.70121](https://doi.org/10.1002/spp2.70121).

## Role and scope

My contribution included planning the quantitative comparison, preparing and checking morphometric measurements, working with the R analysis, producing visualizations, and interpreting the statistical results with the co-authors. The species description and publication are collaborative work.

## License

The source code is released under the [MIT License](LICENSE). The underlying measurements and publication content are not distributed under this license.
