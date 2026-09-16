# Analysis scripts

This directory is reserved for the executable R workflow used to reproduce the project.

Planned canonical script:

`APP23_snRNAseq_complete_analysis.R`

The final script should preserve the analysis actually run for the project, including the non-standard GSE141044 dense-matrix import, QC verification, Seurat preprocessing, resolution 0.5 clustering, UMAP, annotation, edgeR pseudobulk analysis, ranked GO-BP GSEA, DoRothEA/decoupleR TF analysis, and the 24-month CellChat comparison.

The complete executable script is intentionally not reconstructed from prose summaries alone. It should be committed from the exact final R code used for the analysis so that repository code and reported results remain synchronized.
