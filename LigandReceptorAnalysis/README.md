To see what ligand-receptor channels are driving niche signals in our data, we developed niche-LR. Niche-LR uses the [niche-net](https://www.nature.com/articles/s41592-019-0667-5) ligand-target potential matrix to find the top $K$ downstream targets for each ligand. The niche-DE T-statistics of these downstream genes are used to calculate ligand activity scores. The top $M$ ligands by ligand activity score and their corresponding receptors are then tested to confirm expression in the tissue. Niche-LR can be performed on spot resolution data using the function 'niche_LR_spot' and on single cell resolution data using the function 'niche_LR_cell'. 'niche_LR_spot' takes in 9 arguments 

<details>
  <summary>Arguments</summary>
  
+ object: Niche-DE object
+ ligand cell: The cell type that expresses the ligand
+ receptor cell: The cell type that expresses the receptor
+ ligand_target_matrix: A matrix that measures the association between ligands and their downstream target genes. The dimension should be #target genes by #ligands
+ lr-mat: A matrix that matches ligands with their corresponding receptors. This matrix should have two columns. The first will be ligands and the second will be the corresponding receptors
+ K: The number of downstream target genes to use when calculating the ligand activity score
+ M: The maximum number of ligands that can pass initial filtering
+ alpha: The level at which to perform the Benjamini Hochberg correction
+ truncation value: The value at which to truncate T statistics.
</details>
  
We now perform ligand-receptor analysis to infer ligand-receptor interactions between tumor cells (ligand expressing cell) and fibroblasts (receptor expressing cell) . The output will be a list of ligands and their corresponding receptors

```{r}
data("niche_net_ligand_target_matrix")
data("ramilowski_ligand_receptor_list")
fibro_tumor_LR = niche_LR_spot(NDE_obj,ligand_cell = 'tumor_epithelial',receptor_cell = 'stromal',
ligand_target_matrix = niche_net_ligand_target_matrix,
lr_mat = ramilowski_ligand_receptor_list,K = 25,M = 50,alpha = 0.05,truncation_value = 3)
#preview output
head(fibro_tumor_LR)
```
