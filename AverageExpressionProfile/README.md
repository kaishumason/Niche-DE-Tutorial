# Calculating the Average Expression Profile From a scRNA-seq Reference Dataset
Because niche-DE compares observed gene expression against the average expression for a cell type, making an average expression profile matrix is critical. This can be done with the function 'CreateLibraryMatrix' if you have raw data. If your reference dataset is a seurat object, you can use the function 'CreateLibrarymatrixFromSeurat'. This function takes in 2 arguments 

<details>
  <summary>Arguments</summary>
  
  + seurat object: A seurat object
  + assay: The assay from which to extract the counts matrix to calculate the average expression profile
  Note that the cell types of the seurat object are assumed to be available via the command 'Idents(seurat object)'
  
 </details>
  
 ```
 #read in data
 reference = readRDS('liver_met_ref.rds')
 #create library matrix
 CreateLibraryMatrixFromSeurat(reference,assay = 'RNA')
 ```


