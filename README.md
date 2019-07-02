# varactor
Visualization and analysis of single-cell RNA-seq data by alternative clustering

# Introduction
Varactor takes the expression matrix and the alleged nonpreferred clustering, which are either labeled beforehand, or previously discovered from the data. It redefines the pairwise distance of the cells, where the effect of the unwanted clustering is controlled, and use tSNE (which can be substituted with any distance-based clustering methods) on the new distances. It provides a new perspective for inspecting the similarity of the cells, instead of manipulating the expression data. The differential expression analysis may then be performed on the original data (see Nygaard, V. et al. Methods that remove batch effects while retaining group differences may lead to exaggerated confidence in downstream analyses. Biostatistics, 17(1), 29–39 (2016)) with the batches considered either covariates or strata. We implemented stratified Wilcoxon U-test as a stand alone tool, and a supplemnent to the [Seurat](https://github.com/satijalab/seurat) package.

# Usage

## Create a Varactor Object
Varactor is implemented using R6 class. To create an object, simply call ```new()```. The following chunk uses 10x and well-seq of PBMC for example, to create a Varactor object. A label called "sample" is automatically added to the labels to flag the origination of cells, even after they are combined into one matrix (by ```combine()``` showing later).
```r
source("./R/varactor_class.R")
data <- list(x10x = pbmc_10x$expr, well = pbmc_well$expr)
labels <- list(x10x = list(type = as.character(pbmc_10x$cell_type)), 
                           well = list(type = as.character(pbmc_well$cell_type))
                          )
obj2 <- Varactor$new(data = data, labels = labels)
```

## Preprocess
The input is a list of datasets and labels, so preprocessing is necessary to analyze them jointly. This includes normalization (including log-transform) of each dataset, combine them together (while only retain genes appear in all datasets) and dimensional reduction. This can be done by calling the corresponding methods (i.e., member functions).
```r
obj2$normalize()
obj2$combine()
obj2$reduce()
```
Or, you may chain these methods
```r
obj2$normalize()$combine()$reduce()
```

## Primary Embedding
Using Euclidean distance, it is easy to find and plot the most familiar embedding using t-SNE. You may also choose to use UMAP.
```r
obj2$define_metric("primary", "euclidean")$measure("primary")$embed("primary", "tsne")$plot_embedding("primary", "type", pch=20)
```
You can also plot it with a different coloring. The embedding is automatically stored in the object, so you only need to call ```plot_embedding```.
```{r}
obj2$plot_embedding("alternative", "sample", pch=20)
```

## Secondary Embedding
By using a different definition of distance (davidson distance controling difference between samples in this case), you can find the alternative embedding.
```r
obj2$define_metric("alternative", "davidson", strata = "sample")$measure("alternative")$embed("alternative", "tsne")$plot_embedding("alternative", "type", pch=20)
```


# Results
## Datasets
Many good datasets can be found from [Hemberg Group, Sanger Institute](https://github.com/hemberg-lab/scRNA.seq.datasets).

## Brain cells
This experiment show that Varactor can evoke findings on multi-sample data.

Lake, B. B. et al. Neuronal subtypes and diversity revealed by single-nucleus RNA sequencing of the human brain. Science 352, 1586–1590 (2016)

## PBMC cells
This experiment show that Varactor can account for samples assayed by different technologies.

[10x PBMC3k dataset](http://support.10xgenomics.com/single-cell/datasets/pbmc3k)

[Seq-Well PBMC dataset (GSE92495)](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE92495)
