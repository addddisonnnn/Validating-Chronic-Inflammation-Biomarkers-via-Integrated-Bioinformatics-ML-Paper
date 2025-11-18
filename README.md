# Validation-of-Chronic-Inflammation-Biomarkers-via-Integrated-ML-Bioinformatics-Paper
Documenting my progress towards validating and recreating a [paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC12095375/#s1) titled 'Identification and validation of shared biomarkers and drug repurposing in psoriasis and Crohn’s disease: integrating bioinformatics, machine learning, and experimental approaches'.

## Research Problem
Psoriases and Crohn's Disease are two chronic inflammatory conditions that have a myriad of similarities, including shared genetic risk factors, often occuring at the same time in paitents, have overlapping immune dysregulation, and lack shared diagnoistic biomarkers and treaments. Instead of studying each disease separately, scientists wanted to find common molecular mechanisms that could better diagnoses and find existing drugs to test and treat both conditions.

## Key Findings
Li et al. (2025) identified five shared overactive genes in both disease: KIF4A, DLGAP5, NCAPG, CCNB1, and CEP55. These genes are known for controlling cell division and have been linked to immune system problems in these condiitons.  

## Main Steps
1. Procuring Data & Preprocessing
    * What: Download and prepare gene expression datasets from 58 psoriasis patients, 67 Crohn's patients, and healthy controls.
    * Why: Need sick vs. healthy comparison to find disease-related genes
    * Datasets Used: Primary Analysis: GSE13355 (psoriasis) and GSE75214 (Crohn's), Validation: GSE14905 (psoriasis) and GSE102133 (Crohn's), Single-cell: GSE162183 (psoriasis skin) and GSE214695 (Crohn's colon)
    * Preprocessing: Probe-to-gene symbol conversion,background correction and quantile normalization, log2 transformation, quality control with box plots, and removal of non-lesional samples
2. Differential Expression Analysis
    * What: Identify genes that are significantly different between disease and control groups
    * Why: Find out which genes are turned on and off in each disease and identify potential biomarkers
    * Method: Linear models for microarray data (limma)
    * Visualization: PCA plots, volcano, heatmaps

3. Gene Set Enrichment Analysis
    * What: Identify biological pathways that are overrepresented in the disease states
    * Database: MSigDB Hallmark gene sets
    * Visualization: 
    * Why: Understand and discover the biological context of DEGS and pathway similarities between diseases


4. Weighted Gene Co-expression Network Analysis (WGCNA)
    * What: Find groups of genes that work together as functional modules
    * Why: Discover gene networks beyond individual DEGs, identify modules strongly associated with disease traits, and reduce dimensionality while preserving biological meaning
    * Found: 79 key genes that are important in both diseases

5. Functional Enrichment Analysis - Understand What Genes Do
    * What: Understand the biological functions of the 79 shared key genes
    * Why: Figure out what specific genes do and identify key biological processes
    * Method: GO Analysis, KEGG Pathways with the clusterProfile tool
    * Found: They mainly control cell division and immune responses

6. Protein-Protein Interaction Networks - Find Most Important Genes
    * What: Map how the shared genes' proteins interact with each other
    * Why: Identify central hub genes, understand functional relationshaips, and prioritize most biologically important genes
    * Method: STRING Database, MCODE for hub detection
    * Visualization: Cytoscape
    * Found: 18 core hub genes from the 79

7. Machine Learning Biomarker Selection
    * What: Use AI algorithms to select the best diagnostic biomarkers
    * Why: Objectively select most predictive genes, handle high-dimensional data, and optimize diagnostic accuracy
    * Method: Algorithms include RF, SVM, XGBoost, Decision Tree, LASSO, KNN
    * Found: 5 final biomarkers from the 18 hub genes

8. Diagnostic Validation
    * What: Tested if these 5 genes can accurately diagnose both diseases
    * Why: Confirm clinical utility and validate across independent datasets
    * Method: Area Under Curve (AUC) though ROC curves
        * Training (GSE13355, GSE75214)
        * Validation (GSE14905, GSE102133)
    * Result: Excellent diagnostic accuracy (AUC > 0.9)

9. Immune Infiltration Analysis
    * What: Analyze immune cell composition and its relationship to hub genes
    * Why: Understand immune context of biomarkers, link genes to specific immune processes, and explain inflammatory processes
    * Method: Single-sample GSEA, correlation with hub gene expression
    * Found: Connected to T-cells and other immune cells in both diseases

10. Single-Cell RNA Sequencing Analysis
    * What: Looked at which specific cell types use these genes
    * Why: Cellular resolution of gene expression, understand tissue-specific mechanisms, and validate bulk RNA-seq findings
    * Method: Seurat package, UMAP clustering
    * Datasets: GSE162183 (psoriasis skin), GSE214695 (Crohn's colon)
    * Found: Mainly in skin cells (psoriasis) and gut lining cells (Crohn's)

11. Drug Drug Repurposing
    * What: Searched for existing drugs that target these 5 (hub) genes
    * Why: Leverage existing safety data and cost-effective drug discovery
    * Method: DSigBS through ENRICHR
    * Found: Etoposide, Lucanthone, Piroxicam are top candidates

12. Computer Drug Testing
    * What: Simulated how well drugs bind to target proteins
    * Why: Predict binding affinity, support drug selection, and understand binding mechanisms
    * Found: Etoposide binds strongest

13. Experimental Validation
    * What: Tested drugs on human cells in the lab
    * Why: Confirm computational predictions, validate biological effects, and support clinical translation
    * Methods: CCK-8 viability, qRT-PCR gene expression
    * Found: Etoposide reduced disease markers

## Citation
Li X, Cao H, Niu M, Liu Q, Liang B, Hou J, Tu J, Gao J. Identification and validation of shared biomarkers and drug repurposing in psoriasis and Crohn's disease: integrating bioinformatics, machine learning, and experimental approaches. Front Immunol. 2025 May 8;16:1587705. doi: 10.3389/fimmu.2025.1587705. PMID: 40406126; PMCID: PMC12095375.
