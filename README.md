# Example Data Visualizations from my Professional Coding Projects
<i>Since much of the code I wrote as part of my bioinformatics consulting job is proprietary I created a page to at least demonstrate the capabilities.
<i>Presented here: flow cytometry analysis methods (written in R)</i><br>
<i>Additional Pipelines Demonstrations: [Cut-and-Run Seq](https://github.com/The1stMartian/Cut-And-Run-Seq-Demo)</i>

# Flow Cytometry Analysis (R)
Technical Overview:
- Investigation of chimeric antigen receptor NK cells (i.e. <b>CAR-NK cells</b>)
- Purpose was to investigate the efficiency of CAR-NK creation
- Actual R code is proprietary (sorry)

## FC Analysis Libraries Used:<br>
Libraries utilized in my pipeline include:<br>
- flowCore - to create the flowSet data type
- flowAI - automated qc
- flowAssist - flowFrame converter
- flowCore - apply function for flowsets
- flowWorkspace - gatingSets, cytoSets 
- ggcyto - autoplot, ggsave
- ggplot2 - data visualization 
- openCyto - flowClust, flowClust2D
- ggpointdensity - graphing
- uwot - UMAP dimensionality reduction
- cytofkit2 - clustering
- ggridges - Fluorescence density plots
- flowStats - DataFrame to flowFrame converter

## General Schema:
- QC: Raw fluorescence batch comparison
- QC: Fluorescence normalization (gaussNorm)

Gating:
- Non-debris gating
- Singlet gating
- Live cell gating 
- Marker gating (CD45+ > ...)

### Step 1: Raw Batch comparison 
- Examine all markers at the same time for a broad overview of the dataset<br>
![Debris](./fc/batch.jpg)

### Step 2: Fluorescence normalization by warpSet or gaussNorm:
- With multiple samples (each row) it becomes increasingly important to normalize fluorescence distributions prior to gating<br>
- In this comparison, gaussNorm performed best<br>
![Debris](./fc/normComp.jpg)

### Step 3: Large Debris Removal:
- Standard removal of non-cell datapoints<br>
- In this example, I didn't remove the smaller debris as later analysis indicated they were actual cells.<br>
![Debris](./fc/debris.jpg)

### Step 4: Singlet Gating:
- Standard removal of cell doublets<br>
![Singlets](./fc/singlets.jpg)

### Step 5+: CD45+ gating for lymphocytes and subsequent two-color gating:
- Multiple gating steps use 2D gates<br>
- This is an example of multiple gates applid to the same set of cells<br>
![Singlets](./fc/gating.jpg)

### Gating with Multiple Samples:
- Example of reproducibility of the gating strategy across 46 samples<br>
![Singlets](./fc/manySamples.jpg)

### Dimensionality Reduction: tSNE (colors by cluster)
- I tried dimensionality reduction with two different algorithms to see which performed better in terms of computation and distinguishing cell clusters (calculated separately of course). UMAP performed better than tSNS, in accordance with various reports.<br> 
![Singlets](./fc/tsne.png)

### Dimensionality Reduction: UMAP (colors by cluster)
- UMAP projection of the same set of cells<br>
![Singlets](./fc/umap.png)

### Gene expression investigation (UMAP)
- To help identify/verify groups of cells, I colored the UMAP projections according the the level of various cell surface markers.<br> 
![Singlets](./fc/UMAP_grid.png)

### Cluster Identification via Gene Expression Heat Map
- Clustered heat maps cah help show the similarities/differences between clusters<br>
- This plot is marked by cell surface marker, though those would normally be replaced by the corresponding gene label<br>
![Singlets](./fc/clusterTree.jpg)

### Schema:
- The cells we were examining were immunologically naive. Accordingly, there were few highly differentiated cells, necessitating a "flat" gating scheme. 
![Singlets](./fc/schema.jpg)
