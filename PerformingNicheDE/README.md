# Running Niche-DE
Once you have set up your niche_DE object, you can run niche-DE using the function 'niche_DE'. This function takes 5 arguments
+ object: A niche-DE object
+ C: The minimum total expression of a gene across observations needed for the niche-DE model to run.  
+ M: Minimum number of spots containing the index cell type with the niche cell type in its effective niche for (index,niche) niche patterns to be investigated. 
+ Gamma: Percentile a gene needs to be with respect to expression in the index cell type in order for the model to investigate niche patterns for that gene in the index cell
```{r,warning = F}
NDE_obj = niche_DE(NDE_obj)
```
