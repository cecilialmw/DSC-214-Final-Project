# DSC-214-Final-Project
DSC 214 Topological Data Analysis Final Project - Cell Type Hierarchical Clustering
## Project Idea
--hehe

## Files
- DSC_214_Finalized.ipynb
  - Finalized version of the project notebook
- dsc_214.ipynb
  - Original version of the project notebook including discarded ideas, redundant installation/imports etc.
- dsc 214 final project outline.pdf
  - Project outline
- Final report (.pdf)
- Final video presentation slides (.pdf)

## Documentation
The dataset we used is not publicaly available. In order to run **DSC_214_Finalized.ipynb** with your own dataset, please change the variable `file_path` accordingly in the *Data Loading* section.

This project works specifically with single-cell RNA-sequencing data in *.h5ad* format. Therefore, please make sure your dataset is in this format to ensure minimal modification. If you want to load a differnt formatted dataset, please modifiy the function `load_and_process_h5ad()` in the *Functions -> Basic* section accordingly.

This notebook does not support saving plot as a seperate file. You can add this function by modifying the functions `plot_dgm()`, `plot_dendrogram()`, or `persistence_img()`.

## Parameters

