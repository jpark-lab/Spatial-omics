# Spatial Omics: Analysis Frameworks and Tutorial (CosMx Example)

This tutorial introduces key concepts, data structures, and tools for analyzing spatial omics data using Python. It is written with CosMx SMI imaging transcriptomics in mind but generalizes to other platforms. 

## Overview
- Introduce spatial omics data types: imaging-based (e.g. CosMx), sequencing-based (e.g. Visium), and proteomics (e.g. IMC, CODEX).
- Learn about data formats: `AnnData` (Python) and `SpatialExperiment` (R/Bioconductor).
- Explore core Python tools: `scanpy`, `squidpy`, and `napari`.
- Load, explore, and visualize CosMx spatial data using open-source Python packages.

## Quick Links
- [CosMx Flat File Demo Dataset (Lung)](https://nanostring-public-share.s3.us-west-2.amazonaws.com/CosMx/Cellular+Data/Lung5_Rep1-Flat_files_and_images.zip)
- [Squidpy Documentation](https://squidpy.readthedocs.io)
- [Scanpy Documentation](https://scanpy.readthedocs.io)

---

## 1. Introduction to Spatial Omics Data
Spatial omics combines molecular profiles (RNA, protein) with spatial location in tissue. 

**Types:**
- **Imaging-based transcriptomics** (CosMx, MERSCOPE): single-molecule resolution, high-plex, targeted panels.
- **Sequencing-based** (10x Visium, Slide-seq): whole transcriptome coverage, lower resolution.
- **Imaging-based proteomics** (CODEX, IMC): high-resolution, lower feature counts.

---

## 2. Data Structures

### Python: `AnnData`
- `.X` — expression matrix (cells × genes)
- `.obs` — cell metadata (e.g. FOV, area, cluster labels)
- `.var` — gene metadata
- `.obsm['spatial']` — cell coordinates (x, y)
- `.uns` — tissue images, color maps, etc.

### R: `SpatialExperiment`
- `assay()` — expression data
- `colData()` — cell metadata
- `spatialCoords()` — coordinates
- `imgData()` — image storage

---

## 3. Python Tools
- `Scanpy`: preprocessing, clustering, dimensionality reduction
- `Squidpy`: spatial graph analysis, spatial statistics, integration with images
- `Napari`: interactive visualization of spatial omics data and images

---

## 4. Tutorial: CosMx Data Analysis in Python

### 1. Load Data
```python
import squidpy as sq
adata = sq.read.nanostring(
    path="cosmx_data/",
    counts_file="exprMat.csv",
    meta_file="metadata.csv",
    fov_file="fov_positions.csv"
)
```

### 2. Basic Exploration
```python
adata.shape  # (cells, genes)
adata.obs.head()
adata.var.head()
adata.obsm["spatial"][:5]
```

### 3. Preprocessing and Clustering
```python
import scanpy as sc
sc.pp.normalize_total(adata)
sc.pp.log1p(adata)
sc.pp.pca(adata)
sc.pp.neighbors(adata)
sc.tl.umap(adata)
sc.tl.leiden(adata, resolution=0.5)
```

### 4. Spatial Graph and Autocorrelation
```python
sq.gr.spatial_neighbors(adata, coord_type="generic", delaunay=True)
sq.gr.spatial_autocorr(adata, mode='moran')
sq.pl.spatial_scatter(adata, color="GeneX")
```

### 5. Neighborhood Enrichment
```python
sq.gr.nhood_enrichment(adata, cluster_key="leiden")
sq.pl.nhood_enrichment(adata)
```

---

## 5. Student Practice

### Conceptual
- What is the purpose of the spatial neighbors graph?
- How does Moran's I detect spatial patterning?

### Practical
- Where are spatial coordinates stored in an AnnData object?
- How do you visualize a gene's expression in tissue space?

### Analytical
- How would you define spatial domains in a tissue using expression data?
- What biological insights can be derived from spatial clustering or co-localization?

---

## Next Steps
- Extend analysis to full CosMx panels
- Integrate protein and RNA data
- Try other tools: `Giotto`, `Seurat`, `Napari`, `BayesSpace`
- Explore public reference atlases (e.g. HuBMAP, SAHA)

This page can be expanded with more tutorials and methods chapters. Let us know what you'd like to see next!
