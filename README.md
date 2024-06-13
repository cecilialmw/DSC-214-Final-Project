# Classification of Cell Types through Topological Data Analysis of Gene Co-Expression Distance
DSC 214 Topological Data Analysis - Spring 2024

## Instructor
- Zhengchao Wan
  
## Group Member
- Cecilia Liu :doughnut:
- Jason Chen :dna:
- Zixi Yuan :memo:

## Project Idea
We aim to explore the similarities between various cell types through hierarchical clustering, employing topological data analysis (TDA) tools to address this question. Our objective is to discern whether the topological characteristics of genes associated with each cell type are sufficiently distinct to enable differentiation. The initial step involves constructing a filtration where genes serve as vertices; this requires calculating the pairwise distances between genes. In bioinformatics, the gene co-expression network is a widely adopted approach. Drawing on this concept, we construct distinct gene co-expression distance matrices for each cell type, employing various metrics such as Pearson correlation and Euclidean distance.

Upon establishing the Vietoris-Rips filtration from this point cloud data, we obtain a persistence diagram. This diagram allows us to compute the pairwise distances between cell types. We use this final pairwise distance matrix to perform hierarchical clustering, which is then visualized through a dendrogram. Additionally, we explore aggregate hierarchical clustering using aggregate distances, with the aim of achieving more stable and accurate results.

## Files
- **DSC_214_Finalized.ipynb**
  - Finalized version of the project notebook
- **dsc_214.ipynb**
  - Original version of the project notebook including discarded ideas, redundant installation/imports etc.
- **dsc 214 final project outline.pdf**
  - Project outline
- **DSC_214_final_report.pdf**
- **DSC_214_final_report.zip**
  - Include all files
- Final video presentation slides (.pdf)

## Configuration
We run the notebook on google Colab with 51GB RAM. The maximum usage is approximately 50GB. Therefore, if you wish to run this notebook with a larger dataset, especially if the cell count of a perticular cell type is larger than the cell count of the oligodendrocyte in our dataset, you might need to modify the `cell_df()` in *Functions -> Basic* to parallelize the process.

## Documentation
The dataset we used is from *Human Brain Cell Atlas*. In order to run **DSC_214_Finalized.ipynb** with your own dataset, please change the variable `file_path` accordingly in the *Data Loading* section.

This project works specifically with single-cell RNA-sequencing data in *.h5ad* format. Therefore, please make sure your dataset is in this format to ensure minimal modification. If you want to load a different formatted dataset, please modifiy the function `load_and_process_h5ad()` in the *Functions -> Basic* section accordingly.

This notebook does not support saving plot as a seperate file. 
- To save persistent diagram, please modify the function `plot_dgm()` in the *Functions -> Basic* section
- To save persistence image, please modify the function `persistence_img()` in the *Functions -> Persistence Image* section
- To save dendrograms, please modify the function `plot_dendrogram()` in the *Functions -> Basic* section

## Parameters
This notebook supports creating gene co-expression distance using Pearson correlation or Euclidean distance, and comparing persistent diagrams using Bottleneck distance or persistence image. However, there are some pre-defined parameters can be changed to fit your dataset better.

- `cell_df()` in *Functions -> Basic*
  - When `reduce=True`, threshold for downsizing the data for each cell type is currently set to 75%. This means we conly keep the genes that are expressed by more than 75% of the cells of this cell type. You can change this threshold by fiding the elbow point which is implemented in the **dsc_214.ipynb**. However, it's recommended to limit the final gene counts to 2000 to avoid huge computation time.
- `persist_dgm()` in *Functions -> Basic*
  - The current default `maxdim` is 1. You can change it to higher numbers to allow computation of higher dimensional homology. However, the result might be unstable if there is no higher dimentional homology, and it would also increase the computation time.
- `l2_dist_mtrx()` in *Functions -> Distance*
  - This project applies UMAP on the data before calculating the Euclidean distance to avoid the curse of dimensionality. The current setting for UMAP is `(n_neighbors=15, n_components=30, metric='euclidean')`. You can change them based on your preference or using grid search.
  - This project also applies PCA before UMAP, which is a conventional procedure to reduce noise and increase computation efficiency. The current setting kept 99% of the variance. You can change this based on your preference, but please make sure the final number of principle conponents is larger than `n_neighbors` for UMAP.
- `persistence_img_norms()` in *Functions -> Persistence Image*
  - The current setting calculates the 2-norm of the pairwise distance between two persistence images. You can change `p=2` to other numbers to calculate different norms.
- `persistence_img()` in *Functions -> Persistence Image*
  - You can change the `pixel_size`, `birth_range`, `weight_params` accordingly. This can be helpful, for example, if you want to make sure the start-to-end range fits your data. For more customizable options, please check out the `persim` documentaion.
- `persistence_img_resize()` in *Functions -> Persistence Image*
  - This step is crucial because the persistence images are not the same size after fixing the `pixel_size`(resolution). In order to compute the p-norm of their difference, we need to resize them to the same shape. 
  - For the padding option, current target padding size is the largest width and the largest height among all images.
  - For the resize option, the current target new shape is `(10, 3)`. As for our project, the result of resizing persistence image using this option is not ideal. However, it might be a case-by-case situation, expecially with a better shape choice.
  
