scImpute: accurate and robust imputation of scRNA-seq data
================
Difference from Original
-----------
Able to input/output raw matrix data.

```r
# if outfile=raw, returns an imputed matrix instead of outlier
imputed.exp <- scimpute(# full path to raw count matrix
         count_path = count.mat,   # raw count matrix data
         infile = "raw",           # format of input file (genes * cells with header and row.name)
         outfile = "raw",          # format of output file
         out_dir = output.dir,           # full path to output directory
         labeled = FALSE,          # cell type labels not available
         drop_thre = 0.5,          # threshold set on dropout probability
         Kcluster = 2,             # 2 cell subpopulations
         ncores = 10)              # number of cores used in parallel computation
 ```


Original Readme Below
-----------

Wei Vivian Li, Jingyi Jessica Li
2018-06-08

<!-- README.md is generated from README.Rmd. Please edit that file -->
Latest News
-----------

> 2018/06/08:

-   Version 0.0.7 is released!
-   New option for application on TPM values.

Introduction
------------

`scImpute` is developed to accurately and robustly impute the dropout values in scRNA-seq data. `scImpute` can be applied to raw read count matrix before the users perform downstream analyses such as

-   dimension reduction of scRNA-seq data
-   normalization of scRNA-seq data
-   clustering of cell populations
-   differential gene expression analysis
-   time-series analysis of gene expression dynamics

The users can refer to our paper [An accurate and robust imputation method scImpute for single-cell RNA-seq data](https://www.nature.com/articles/s41467-018-03405-7) for a detailed description of the modeling and applications.

Any suggestions on the package are welcome! For technical problems, please report to [Issues](https://github.com/Vivianstats/scImpute/issues). For suggestions and comments on the method, please contact Wei (<liw@ucla.edu>) or Dr. Jessica Li (<jli@stat.ucla.edu>).

Installation
------------

The package is not on CRAN yet. For installation please use the following codes in `R`

``` r
install.packages("devtools")
library(devtools)

install_github("Vivianstats/scImpute")
```

Quick start
-----------

`scImpute` can be easily incorporated into existing pipeline of scRNA-seq analysis. Its only input is the raw count matrix with rows representing genes and columns representing cells. It will output an imputed count matrix with the same dimension. In the simplest case, the imputation task can be done with one single function `scimpute`:

``` r
scimpute(# full path to raw count matrix
         count_path = system.file("extdata", "raw_count.csv", package = "scImpute"), 
         infile = "csv",           # format of input file
         outfile = "csv",          # format of output file
         out_dir = "./",           # full path to output directory
         labeled = FALSE,          # cell type labels not available
         drop_thre = 0.5,          # threshold set on dropout probability
         Kcluster = 2,             # 2 cell subpopulations
         ncores = 10)              # number of cores used in parallel computation
```

This function returns the column indices of outlier cells, and creates a new file `scimpute_count.csv` in `out_dir` to store the imputed count matrix. Please note that we recommend applying scImpute on the whole-genome count matrix. A filtering step on genes is acceptable but most genes should be present to ensure robust identification of dropouts.

For detailed usage, please refer to the package [manual](https://github.com/Vivianstats/scImpute/blob/master/inst/docs/) or [vignette](https://github.com/Vivianstats/scImpute/blob/master/vignettes/scImpute-vignette.Rmd).

Updates
-------
> 2018/03/16:

-   Version 0.0.6 is released!
-   The scImpute method is published at [*Nature Communications*](https://www.nature.com/articles/s41467-018-03405-7).
-   scImpute now supports input and output in the format of R objects (.rds).

> 2018/01/12:

-   Version 0.0.5 is released!
-   It is now possible to apply scImpute on just one cell population by setting `Kcluster = 1`.

> 2017/10/27:

-   Version 0.0.4 is released!
-   scImpute now supports multi-code parallelism.

> 2017/10/22:

-   Version 0.0.3 is released!
-   Estimation of dropout probabilities is more accurate.
-   Imputation step is more robust.
-   `scimpute()` incorporates a new parameter `Kcluster` to specify the number of cell subpopulations.
-   `scImpute` is now able to detect outlier cells.

> 2017/07/01:

-   Version 0.0.2 is released!
-   This version speeds up the first step in `scImpute` and program now completes in a few seconds when applied to a dataset with 10,000 genes and 100 cells (using single core).
