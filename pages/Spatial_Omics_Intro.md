# Spatial Omics Foundations: Data Types, Formats, and Toolkits

This page introduces the foundational concepts of spatial omics data analysis, including types of spatial omics technologies, data formats, and major analysis ecosystems in Python and R.

---

## 1. Spatial Omics Data Types

### A. Imaging-Based Transcriptomics
- **CosMx SMI (NanoString)**, **MERSCOPE (Vizgen)**, **seqFISH**: use fluorescence microscopy to detect individual RNA molecules.
- Offer single-cell or subcellular resolution.
- Typically target up to ~1000 genes (custom or vendor panels).

### B. Sequencing-Based Spatial Transcriptomics
- **10x Visium**, **Slide-seq**, **Stereo-seq**: use barcoded surfaces to capture transcripts from tissue sections.
- Whole transcriptome coverage, but at lower resolution.
- Spot sizes range from ~2 µm (Stereo-seq) to ~55 µm (Visium).

### C. Imaging-Based Spatial Proteomics
- **CODEX (Akoya)**, **IMC (Fluidigm)**, **MIBI**, **CellScape**: detect proteins using iterative imaging or metal-conjugated antibodies.
- Single-cell to subcellular resolution.
- Multiplexing limit of ~30–60 proteins.

---

## 2. Data Formats

### A. Python: `AnnData`
Standard container for single-cell and spatial omics data.

- `.X`: expression matrix (cells × genes)
- `.obs`: cell metadata (e.g. `cell_type`, `fov`, `total_counts`)
- `.var`: gene metadata (e.g. `gene_id`, `target_name`)
- `.obsm['spatial']`: cell spatial coordinates
- `.uns`: unstructured metadata (images, color maps, annotations)

Also used by:
- **Scanpy**: expression analysis
- **Squidpy**: spatial analysis
- **Napari**: image and segmentation overlay

### B. R/Bioconductor: `SpatialExperiment`
Built on `SummarizedExperiment` and `SingleCellExperiment`.

- `assay()`: expression counts
- `colData()`: cell/spot metadata
- `spatialCoords()`: spatial position of observations
- `imgData()`: image(s) associated with spatial samples

Used by:
- **spatialLIBD**
- **Seurat (via import/export)**
- **Giotto**

Conversion between formats is possible via `zellkonverter` or `SeuratDisk`.

---

## 3. Analysis Ecosystems

### A. Python Tools

- **Scanpy**: normalization, clustering, PCA/UMAP, differential expression
- **Squidpy**: spatial graph construction, spatial statistics (e.g. Moran's I), neighborhood enrichment, image feature extraction
- **Napari**: nD image viewer with support for segmentation masks and spatial overlays

### B. R/Bioconductor Tools

- **SpatialExperiment**: data infrastructure for spatial data
- **spatialLIBD**: visualization for spatial transcriptomics (Visium focus)
- **Seurat v5**: supports CosMx, MERSCOPE, CODEX, and Visium data loading and analysis
- **Giotto**: complete spatial omics platform with web viewer and advanced stats

---

## 4. Summary
- Imaging-based methods offer high resolution but use targeted panels.
- Sequencing-based methods provide transcriptome-wide coverage but at lower resolution.
- `AnnData` and `SpatialExperiment` are the core infrastructures.
- Python and R each offer mature, complementary toolsets.

For hands-on practice, see the [CosMx Tutorial](tutorial_cosmx.md) page.