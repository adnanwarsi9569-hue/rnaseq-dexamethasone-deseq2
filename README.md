# RNA-Seq Differential Expression: Dexamethasone in Airway Smooth Muscle Cells

Differential expression analysis in R (DESeq2) of public RNA-Seq dataset GSE52778,
with FastQC quality control, volcano plot, heatmap, GO enrichment and a reproducible
R Markdown report.

Built for the OpenBluff Bioinformatics Internship (Task 2).

## Dataset

GSE52778 (Himes et al., 2014): human airway smooth muscle cells from 4 donors, untreated
vs treated with 1 uM dexamethasone for 18 h (8 samples). Gene-level counts are from the
Bioconductor `airway` package.

## Workflow

1. Quality control with FastQC (first 100,000 reads of one untreated and one treated sample)
2. Filtering: genes with at least 10 reads in at least 4 samples
3. Normalisation and testing with DESeq2, model `~ cell + dex`
4. Visualisation: PCA, volcano plot, heatmap of top 30 genes
5. GO Biological Process enrichment with topGO (Fisher, weight01)

## Key results

- 15,826 genes tested after filtering
- 951 differentially expressed genes (adjusted p < 0.05, |log2FC| >= 1): 490 up, 461 down
- FastQC: both samples passed 10 of 11 modules; warning for overrepresented sequences only
- Top GO terms: angiogenesis, extracellular matrix organisation, retinol metabolism, immune response

## Files

- `Task2_RNAseq_DESeq2.Rmd` : R Markdown source
- `Task2_RNAseq_DESeq2.html` : rendered report
- `results/DE_results.csv` : full DESeq2 results
- `results/GO_BP_enrichment.csv` : top GO terms
- `results/fastqc/` : FastQC reports

## How to run

    Rscript -e 'rmarkdown::render("Task2_RNAseq_DESeq2.Rmd")'

R packages: DESeq2, airway, org.Hs.eg.db, topGO, GO.db, ggplot2, ggrepel, pheatmap, dplyr, rmarkdown.

## Limitations

Only 4 donors and one cell type; counts come from the `airway` package and were not
re-aligned from raw reads; FastQC was run on a subset of reads from two samples.

## Author

Adnan Warsi
