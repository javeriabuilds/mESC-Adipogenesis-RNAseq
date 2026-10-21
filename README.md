# Exploratory RNA-seq Reanalysis of Mouse Embryonic Stem Cell Adipogenesis

## Project Overview

This project presents an exploratory bioinformatics reanalysis of gene-expression patterns associated with differentiation in mouse embryonic stem cells (mESCs).

Using a processed variance-stabilized expression matrix, the analysis compares non-differentiating (Neg) and differentiating (Pos) samples to investigate condition-associated expression patterns, identify differentially expressed genes, and explore biological processes represented in the results.

The project brings together sample-level quality assessment, exploratory visualization, differential-expression screening, Gene Ontology (GO) enrichment, and selected gene-set enrichment analysis.

**Analysis type:** Secondary-data reanalysis  
**Organism:** *Mus musculus* (house mouse)  
**Data type:** Processed RNA-seq gene-expression matrix  
**Experimental groups:** Neg and Pos, three samples per group

## Research Question

What gene-expression patterns and biological processes distinguish the differentiating and non-differentiating mouse embryonic stem cell samples in this dataset?

## Dataset and Provenance

The analysis uses a processed variance-stabilized expression matrix associated with the mESC adipogenesis research dataset.

- **NCBI BioProject:** [PRJNA1126392](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA1126392)
- **NCBI SRA study:** [SRP515101](https://www.ncbi.nlm.nih.gov/sra?term=SRP515101)
- **Processed expression matrix source:** The publicly available `vst_matrix_genes.csv` file in the Al-Sayegh Lab-associated GitHub project.

The input matrix contains six samples: Neg_1, Neg_2, Neg_3, Pos_1, Pos_2, and Pos_3.

This project analyzes an existing processed expression matrix. It does not generate new sequencing data or independently reproduce the original raw-read processing pipeline.

## Analysis Workflow

The Jupyter notebook documents the analysis and its results.

1. **Data inspection and quality assessment:** Examine the expression matrix and assess sample-level expression patterns.
2. **Exploratory visualization:** Use principal component analysis (PCA) to examine relationships among samples.
3. **Differential-expression screening:** Apply row-wise Welch's t-tests to variance-stabilized expression values and adjust p-values for multiple testing using the Benjamini–Hochberg procedure.
4. **Expression visualization:** Examine differential-expression patterns using a volcano plot and heatmap.
5. **Gene Ontology enrichment:** Perform direction-specific GO Biological Process over-representation analysis.
6. **Gene-set enrichment:** Investigate selected gene sets using ranked expression statistics.
7. **Interpretation and limitations:** Integrate the results while accounting for sample size, preprocessing, annotation and statistical limitations.

## Key Findings

### Differential-expression screening

The analysis identified **1,089 matrix rows with Benjamini–Hochberg-adjusted p-values below 0.05**:

- 344 rows showed higher mean expression in Pos than in Neg.
- 745 rows showed lower mean expression in Pos than in Neg.

These are row-level counts. Duplicate gene symbols mean that the number of significant rows should not automatically be interpreted as the number of unique genes.

### Gene Ontology enrichment

Direction-specific GO Biological Process analysis identified:

- **6 significant terms** among genes with higher expression in Pos.
- **97 significant terms** among genes with lower expression in Pos.

Annotations among the higher-expression set included nervous-system-development-related processes. The lower-expression set included epithelial differentiation and structural-organization-related processes.

GO enrichment indicates statistical over-representation of annotations; it does not independently demonstrate activation or suppression of a biological process.

### Selected gene-set enrichment

The selected gene-set enrichment analysis reported the following results:

- **Epithelial cell differentiation:** NES = −2.077; FDR q-value reported as 0.000 at displayed precision.
- **Extracellular matrix organization:** NES = −0.996; FDR q-value = 0.460.
- **Phospholipid metabolic process:** NES = −1.638; FDR q-value = 0.175.
- **Adipose tissue development:** NES = −1.018; FDR q-value = 0.440.

Using the Pos-minus-Neg ranking, negative normalized enrichment scores (NES) indicate enrichment toward the lower-in-Pos end of the ranking. Epithelial cell differentiation met the FDR < 0.05 significance threshold, whereas the other three selected gene sets did not. These findings are exploratory and do not establish causal mechanisms or confirm that the observed expression changes are specific to adipogenic differentiation.

## Limitations

Several limitations are important when interpreting these findings:

- The analysis includes only three samples per condition.
- The input is a processed variance-stabilized expression matrix, not raw RNA-seq counts.
- Welch's t-tests on variance-stabilized values are exploratory and are not equivalent to differential-expression modelling with a count-based method such as DESeq2 or edgeR.
- Duplicate gene symbols and annotation coverage can affect gene-level interpretation and enrichment results.
- The findings have not been independently validated in this project.

The results should therefore be treated as hypothesis-generating. Further work using the original raw counts, an appropriate count-based statistical model, and independent validation would strengthen the conclusions.

## Reproducibility

The primary analysis artifact is [`mESC_Adipogenesis_RNAseq_Final_Submission.ipynb`](./mESC_Adipogenesis_RNAseq_Final_Submission.ipynb).

To inspect the analysis:

1. Open the notebook on GitHub to review its code, explanations, outputs and visualizations.
2. To execute it, download the notebook and open it in Jupyter or upload it to Google Colab.
3. Ensure the required input expression matrix is available at the location expected by the notebook.
4. Install the Python packages imported by the notebook if they are not already installed.
5. Run the notebook from top to bottom.

Exact reproduction requires access to the same input matrix and compatible package versions. The notebook documents the methods, checks and interpretive limitations of this exploratory reanalysis.

## Scope of the Project

This is an independent, exploratory reanalysis of publicly available research data. It is intended to demonstrate engagement with transcriptomic data analysis, statistical interpretation, biological enrichment methods, and reproducible computational research. It is not presented as a new experimental study or as a definitive validation of adipogenic differentiation mechanisms.
