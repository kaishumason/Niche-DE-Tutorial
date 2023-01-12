
Starting with a spatial seurat object, we can make a niche-DE object with the function 'CreateNicheDEObjectFrom Seurat'. This function takes in 5 arguments
<details>
  <summary>Arguments</summary>
  
  + seurat object: A seurat object
  + assay: The assay from which to retrieve the counts matrix. Will be taken from slot 'counts'
  + library mat: The average expression profile matrix calcculated from a reference dataset
  + deconv mat: The deconvolution matrix for the spatial dataset
  + sigma: A list of kernel bandwidths to use for effective niche calculation
  
  </details>

```
#read in seurat object
seurat_obj = readRDS('liver_met_seurat.rds')
#download average expression profile matrix 
data("vignette_library_matrix")
data("vignette_deconv_mat")
#make niche-DE object
NDE_obj = CreateNicheDEObject(seurat_obj,'Spatial',vignette_library_matrix,vignette_deconv_mat,sigma = c(1,15,40))

```
