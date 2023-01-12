Starting with a spatial seurat object, we can make a niche-DE object with the function 'CreateNicheDEObjectFrom Seurat'. This function takes in 5 arguments
<details>
  <summary>Arguments</summary>
  
  + seurat object: A seurat object
  + assay: The assay from which to retrieve the counts matrix. Will be taken from slot 'counts'
  + library mat: The average expression profile matrix calcculated from a reference dataset
  + deconv mat: The deconvolution matrix for the spatial dataset
  + sigma: A list of kernel bandwidths to use for effective niche calculation
  
  </details>
