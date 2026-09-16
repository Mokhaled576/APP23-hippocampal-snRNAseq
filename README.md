# APP23 hippocampal single-nucleus RNA-seq

Reproducible analysis of hippocampal neuronal subtype-specific transcriptional remodeling in the APP23 mouse model using GEO dataset **GSE141044**.

## Study overview

This repository contains the analysis workflow used to examine age- and neuronal-subtype-dependent transcriptional remodeling in APP23 hippocampal neurons. The analysis starts from the processed expression matrix deposited with GSE141044 and includes quality-control verification, Seurat normalization and clustering, UMAP visualization, neuronal annotation, mouse-level pseudobulk differential expression, ranked GO Biological Process GSEA, transcription-factor activity inference, and CellChat-based descriptive neuron-to-neuron communication analysis.

The primary biological question is: **Which hippocampal neuronal subtypes exhibit the strongest pathway-level transcriptional remodeling in APP23 mice, and which biological programs distinguish susceptible from relatively preserved neuronal populations?**

## Dataset

- GEO accession: `GSE141044`
- Organism: *Mus musculus*
- Starting processed dataset: 3,280 neuronal nuclei from 11 biological samples
- Ages: 6 months and 24 months
- Genotypes: WT and APP23
- Source publication: Zhong et al. (2020), *Single-nucleus RNA sequencing reveals transcriptional changes of hippocampal neurons in APP23 mouse model of Alzheimer's disease*.

Large GEO source files are intentionally not stored in this repository. See `data/README.md` for acquisition details.

## Analysis outline

1. Import and metadata construction
2. QC verification
3. Log normalization and 2,000 highly variable genes
4. PCA and graph-based clustering
5. UMAP visualization (no t-SNE is used in this project)
6. Fine-cluster marker analysis and broad neuronal annotation
7. Mouse-level pseudobulk differential expression with edgeR
8. Ranked GO Biological Process GSEA with clusterProfiler
9. TF activity inference with DoRothEA/decoupleR and sample-level testing with limma
10. Descriptive 24-month WT versus APP23 CellChat analysis

## Broad neuronal populations

The primary inferential analyses use four broad neuronal populations: `DG`, `CA1_like`, `CA3`, and `Inhibitory`. The finer 10-cluster solution is retained for exploratory visualization and marker characterization.

## Reproducibility notes

Biological replication is defined at the mouse/sample level rather than treating individual nuclei as independent replicates. No Harmony/integration correction is applied in the primary workflow. The processed matrix contains no mitochondrial features suitable for mitochondrial-percentage filtering. Primary pathway and TF ranking sensitivity analyses exclude exact uppercase `APP` and `Thy1` because these signals are closely associated with the APP23 construct; endogenous title-case `App` is retained.

CellChat is interpreted descriptively because condition-level objects pool nuclei across biological samples and because the dataset contains neuronal nuclei only; inferred signaling therefore represents neuron-to-neuron communication rather than the full hippocampal cellular environment.

## Repository structure

```text
APP23-hippocampal-snRNAseq/
├── README.md
├── .gitignore
├── CITATION.cff
├── data/
│   └── README.md
├── scripts/
│   └── README.md
├── results/
│   └── README.md
├── figures/
│   ├── main/
│   └── supplementary/
└── docs/
    ├── METHODS.md
    └── ANALYSIS_WORKFLOW.md
```

## Current biological summary

The analysis supports subtype- and age-dependent remodeling. DG neurons show early pathway-level depletion of synaptic transmission/vesicle programs and later synaptic/structural remodeling. CA1-like neurons show pronounced cholesterol/sterol-associated pathway enrichment at 24 months. CA3 and inhibitory populations show comparatively limited FDR-significant pathway changes under the primary ranked-GSEA criterion. TF activity analysis is exploratory after multiple-testing correction, while CellChat indicates broader reorganization of inferred neuronal communication rather than a uniform increase in signaling.

## Status

The repository is currently private while the manuscript and final analysis documentation are being finalized. Analysis scripts, result tables, and manuscript figures will be added in reproducible repository form without committing large raw data or large serialized R objects.
