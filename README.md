# APP23 hippocampal single-nucleus RNA-seq

Reproducible analysis of hippocampal neuronal subtype-specific transcriptional remodeling in the APP23 mouse model using GEO dataset **GSE141044**.

## Study overview

This repository contains the completed course-project analysis examining age- and neuronal-subtype-dependent transcriptional remodeling in APP23 hippocampal neurons. The workflow starts from the processed GSE141044 expression matrix and includes QC verification, Seurat normalization and clustering, UMAP visualization, neuronal annotation, mouse-level pseudobulk differential expression, ranked GO Biological Process GSEA, transcription-factor activity inference, and descriptive CellChat neuron-to-neuron communication analysis.

**Primary question:** Which hippocampal neuronal subtypes exhibit the strongest pathway-level transcriptional remodeling in APP23 mice, and which biological programs distinguish susceptible from relatively preserved neuronal populations?

## Dataset

- GEO accession: `GSE141044`
- Organism: *Mus musculus*
- Starting processed dataset: 3,280 neuronal nuclei from 11 biological samples
- Ages: 6 and 24 months
- Genotypes: WT and APP23
- Source publication: Zhong et al. (2020), *Single-nucleus RNA sequencing reveals transcriptional changes of hippocampal neurons in APP23 mouse model of Alzheimer's disease*.

Large GEO source files are intentionally not stored in this repository. See `data/README.md` for acquisition details.

## Analysis workflow

1. Non-standard GSE141044 dense-matrix import and metadata construction
2. QC verification
3. Log normalization and selection of 2,000 highly variable genes
4. PCA and graph-based clustering
5. UMAP visualization (**no t-SNE**)
6. Fine-cluster marker analysis and broad neuronal annotation
7. Mouse-level pseudobulk differential expression with edgeR
8. Ranked GO Biological Process GSEA with clusterProfiler
9. TF activity inference with DoRothEA/decoupleR and sample-level testing with limma
10. Descriptive 24-month WT-versus-APP23 CellChat analysis

The complete analysis history is preserved in `scripts/GSE141044_APP23_full_project.R`.

## Broad neuronal populations

Primary inferential analyses use four broad populations: `DG`, `CA1_like`, `CA3`, and `Inhibitory`. The 10-cluster solution is retained for exploratory visualization and marker characterization.

## Main findings

APP23-associated remodeling is subtype- and age-dependent. DG neurons show early depletion of synaptic transmission and synaptic-vesicle programs and later synaptic/structural remodeling. CA1-like neurons show pronounced cholesterol/sterol-associated pathway enrichment at 24 months. CA3 and inhibitory populations show comparatively limited FDR-significant pathway changes under the primary ranked-GSEA criterion.

TF activity inference produced no FDR-significant differential TF activities; Srebf2 is therefore treated only as an exploratory candidate consistent with the late CA1-like sterol program. CellChat indicates reorganization of inferred neuronal communication rather than a uniform increase in signaling, including altered cholesterol/desmosterol-associated signaling.

See `docs/RESULTS_SUMMARY.md` for a concise interpretation and limitations.

## Reproducibility notes

Biological replication is defined at the mouse/sample level rather than treating individual nuclei as independent replicates. No Harmony/integration correction is applied in the primary workflow. The processed matrix contains no mitochondrial features suitable for mitochondrial-percentage filtering. Primary pathway and TF ranking sensitivity analyses exclude exact uppercase `APP` and `Thy1` because these signals are closely associated with the APP23 construct; endogenous title-case `App` is retained.

CellChat is interpreted descriptively because condition-level objects pool nuclei across biological samples and the dataset contains neuronal nuclei only. Inferred signaling therefore represents neuron-to-neuron communication rather than the full hippocampal cellular environment.

## Repository structure

```text
APP23-hippocampal-snRNAseq/
├── README.md
├── .gitignore
├── CITATION.cff
├── data/
│   └── README.md
├── scripts/
│   ├── README.md
│   └── GSE141044_APP23_full_project.R
├── results/
│   ├── README.md
│   └── CellChat/...
├── figures/
│   ├── main/
│   │   ├── Figure_1_combined.png
│   │   ├── Figure_1A_UMAP_10_clusters.png
│   │   ├── Figure_1B_UMAP_broad_subtypes.png
│   │   ├── Figure_1C_marker_DotPlot.png
│   │   ├── Figure_2_pathway_remodeling.png
│   │   ├── Figure_3_CellChat_strength_difference.png
│   │   └── Figure_4_Cholesterol_Desmosterol_CellChat.png
│   └── supplementary/
│       ├── APP23_snRNAseq_Supplementary_Figures_FINAL.pdf
│       └── APP23_snRNAseq_Supplementary_Figures_FINAL.docx
└── docs/
    ├── METHODS.md
    ├── ANALYSIS_WORKFLOW.md
    ├── RESULTS_SUMMARY.md
    └── APP23_snRNAseq_full_manuscript_draft.docx
```

## Repository status

The full R analysis script, final main figures, assembled supplementary figures, manuscript draft, methods/workflow documentation, and version-controlled summary results are deposited here. Raw GEO files and large serialized R objects are intentionally excluded.

The repository can remain private while the manuscript/course submission is being finalized and can be made public later if desired.