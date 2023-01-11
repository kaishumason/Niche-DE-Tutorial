
<details>
  <summary>Suggestions on choice of kernel bandwidth</summary>
  
  # Choice of sigma/kernel bandwidth
Choosing a reasonable sigma vector is critical to generating robust and interpretable results.Sigma essentially determines what range of neighboring spots contribute towards the effective niche. Small values of sigma ensure that only close neighboring spots are considered while large values of sigma result in effective niches that are smooth across large regions of the tissue.\
To see what this looks like, I will generate a grid of values and show what spots contribute to the effective niche of the middle spot. The size of the spot corresponds to its relative importance. 

```{r}
#generate coordiantes
coord = expand.grid(c(1:20),c(1:20))
colnames(coord) = c('x','y')
#get distance matrix
D = as.matrix(dist(coord,method = 'euclidean',diag = T))
#extract center distances
D = D[190,]
coord = data.frame(coord,D)
```
We first see what happens if the kernel bandwidth is very small. We see that the only spot that contributes to the effective niche is the middle spot itself. This may be appropriate if the spot can contain many cells like in Visium data.

```{r}
#input your own sigma value
sigma = 0.001
coord_sigma_small = coord
coord_sigma_small$D = exp(-coord_sigma_small$D^2/sigma^2)
coord_sigma_small$D[coord_sigma_small$D<0.05] = 0
library(ggplot2)
ggplot(coord_sigma_small,aes(x,y,size=ifelse(D==0, NA, D)))+geom_point()+ theme(legend.position="none")
```
We now see what happens if the kernel bandwidth is equivalent to the distance between neighboring spots. We see that neighboring spots now also contribute to the effective niche. This value may be appropriate if we believe that niche patterns only depend on the closest neighbors of a spot. 

```{r}
#input your own sigma value
sigma = 1
coord_sigma_small = coord
coord_sigma_small$D = exp(-coord_sigma_small$D^2/sigma^2)
coord_sigma_small$D[coord_sigma_small$D<0.05] = 0
library(ggplot2)
ggplot(coord_sigma_small,aes(x,y,size=ifelse(D==0, NA, D)))+geom_point()+ theme(legend.position="none")
```

We now see what happens if the kernel bandwidth is large, say 1/4th of the length of the tissue. Many spots now contribute to the effective niche. Additionally,it looks as though there is nearly equal contribution for many cells near the center. This value may be appropriate if we believe that niche patterns only depend on tissue level patterns in niche.


```{r}
#input your own sigma value
sigma = 5
coord_sigma_small = coord
coord_sigma_small$D = exp(-coord_sigma_small$D^2/sigma^2)
coord_sigma_small$D[coord_sigma_small$D<0.05] = 0
library(ggplot2)
ggplot(coord_sigma_small,aes(x,y,size=ifelse(D==0, NA, D)))+geom_point()+ theme(legend.position="none")
```


Clearly the choice of sigma can affect what niche patterns you will find. For spot data which can contain many cells like Visium, we recommend using a sigma vector that contains a small value, a value equal to the distance between neighboring spots, and a value somewhat larger, say 2-3 times the distance between neighboring spots.
</details>
