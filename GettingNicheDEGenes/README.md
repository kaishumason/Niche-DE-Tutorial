
# Calculating Niche-DE Pvalues

After performing niche-DE we will now calculate pvalues. The function to calculate pvalues is called 'get_niche_DE_pval' and contains two arguments. 
+ object: A niche-DE object
+ pos: A logical indicating if one wants to compute interaction level pvalues corresponding to a gene being an $(index,niche)+$ gene (pos = T), or an $(index,niche)-$ gene (pos = F)
In general, the user should run this function twice, one for each value of 'pos'
```{r,warning=FALSE}
NDE_obj = get_niche_DE_pval(NDE_obj,pos = T)
NDE_obj = get_niche_DE_pval(NDE_obj,pos = F)
```

# Extract Niche-DE Genes For a Specific (Index,Niche) Pair
 After calculating pvalues, we can find which genes are $(index,niche)$ niche genes at varying resolutions and FDR control levels. The function to do so is called 'get_niche_DE_genes' and contains 6 arguments
+ object: A niche-DE object
+ resolution: The resolution at which  to return genes. There are three choices for resolution;gene level, cell type level, and interaction level.
+ index: The index cell type of interest
+ niche: The niche cell type of interest
+ pos:  A logical indicating if one wants to find interaction level $(index,niche)+$ niche genes (pos = T), or $(index,niche)-$ niche genes (pos = F)
+ alpha: The level at which to perform the benjamini-hochberg procedure at each resolution level\
Below, we find interaction level (fibroblast,tumor)+ niche genes.
```{r,warning=FALSE}
get_niche_DE_genes(NDE_obj,'interaction',index='stromal',niche = 'tumor_epithelial',pos = T,alpha = 0.05)
```
The output is a list of genes and their corresponding pvalues at the resolution specified.

<details>
  <summary>Interpretting Your Results</summary>
  Assume that the 'pos' parameter is set to 'True'. The interpretation of your output will differ based on the resolution chosen.\
  + Resolution  gene: Genes outputted show some sign of being a noche gene for some $(index,niche)$ pair.
  + Resolution  cell type: Genes outputted are significantly niche up or down regulated in the index cell. The niche cell type is unknown.
  + Resolution  interaction: Genes outputted are significantly upregulated in the index cell type when in the presence of the niche cell type. If 'pos' = 'False' then Genes outputted are significantly downregulated in the index cell type when in the presence of the niche cell type.
  
  
  <details>
  

