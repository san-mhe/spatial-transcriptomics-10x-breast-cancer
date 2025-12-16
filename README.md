# Spatial Transcriptomics Analysis of Breast Cancer Tissue
### Domain Identification and Spatial Interaction Mapping Using 10x Visium Data

## Overview

This project presents a reproducible spatial transcriptomics analysis pipeline applied to a 10x Genomics Visium breast cancer tissue section. The workflow focuses on rigorous quality control, transcriptional domain discovery, and quantitative spatial interaction analysis to characterise tumour microenvironment architecture.

The analysis is designed to reflect systems-level spatial biology approaches commonly used in research institutes such as A*STAR Genome Institute of Singapore (GIS).

---

## Dataset

- **Technology:** 10x Genomics Visium Spatial Transcriptomics  
- **Tissue:** Human breast cancer tissue (Block A, Section 1)  
- **Data type:** Spot-level gene expression with spatial coordinates  
- **Spots after QC:** ~3,700  
- **Genes (pre-HVG):** ~36,000  

---

## Objectives

- Perform stringent quality control while preserving spatial continuity  
- Identify highly variable genes (HVGs) for downstream analysis  
- Detect transcriptionally distinct spatial domains using graph-based clustering  
- Quantify spatial relationships between domains via neighborhood enrichment and co-occurrence analysis  

---

## Analysis Workflow

### 1. Quality Control
- Evaluation of total UMI counts, detected genes per spot, and mitochondrial read percentage  
- Conservative pass/fail filtering to remove low-quality peripheral spots  

### 2. Normalization & Feature Selection
- Library size normalization and log-transformation  
- HVG selection using Seurat v3 methodology (top 3,000 genes)  

### 3. Dimensionality Reduction & Graph Construction
- Principal component analysis (PCA) on HVGs  
- k-nearest neighbor (kNN) graph construction in expression space  

### 4. Domain Identification
- Leiden clustering applied to the kNN graph (resolution = 0.5)  
- Spatial visualization of transcriptional domains  

### 5. Spatial Interaction Analysis
- Neighborhood enrichment analysis to assess adjacency bias between domains  
- Distance-dependent spatial co-occurrence analysis to quantify short- and long-range spatial relationships  

---

## Key Figures

| Figure | Description | Filename |
|------|------------|----------|
| Fig 1 | QC distributions (UMIs, genes, mitochondrial %) | `figures/01_qc_distributions.png` |
| Fig 2 | Spatial QC metrics over histology | `figures/02_spatial_qc_metrics.png` |
| Fig 3 | QC pass/fail visualization | `figures/03_qc_pass_fail.png` |
| Fig 4 | Highly variable gene selection | `figures/04_hvg_selection.png` |
| Fig 5 | PCA variance explained | `figures/05_pca_variance.png` |
| Fig 6 | Spatial domains (Leiden r = 0.5) | `figures/08_spatial_leiden_r05.png` |
| Fig 7 | Neighborhood enrichment | `figures/11_nhood_enrichment_leiden_r0_5.png` |
| Fig 8 | Spatial co-occurrence | `figures/12_co_occurrence_leiden_r0_5.png` |

---

## Biological Interpretation

- Several domains exhibit strong spatial self-enrichment, consistent with cohesive epithelial/tumour or immune niches  
- Other domains display broader spatial overlap, suggestive of interface or transitional regions  
- Observed spatial structure is not driven by QC artefacts, supporting biological relevance  

These results support a model of spatially organized tumour microenvironments rather than homogeneous mixing.


# Data notes

This repository does not include raw 10x Visium outputs or processed `.h5ad` files due to GitHub file size limits.

## How to reproduce
1. Download the 10x Genomics Visium Breast Cancer dataset (Block A, Section 1) from the official 10x Genomics resource.
2. Place the Space Ranger `outs/` directory at:
   `data/visium_breast_cancer_blockA_section1/outs/`
3. Run notebooks in order:
   - `notebooks/01_load_qc.ipynb`
   - `notebooks/02_norm_hvg_pca_graph.ipynb`
   - `notebooks/03_clustering_domains.ipynb`
   - `notebooks/04_spatial_interactions.ipynb`

All figures in `figures/` can be regenerated deterministically.


