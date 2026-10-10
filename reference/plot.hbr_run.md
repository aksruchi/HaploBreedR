# Plot an hbr_run object

Plot an hbr_run object

## Usage

``` r
# S3 method for class 'hbr_run'
plot(x, type = c("gene_list", "haplotype", "ld_decay"), gene = NULL, ...)
```

## Arguments

- x:

  An hbr_run object.

- type:

  Character. \`"gene_list"\`, \`"haplotype"\`, or \`"ld_decay"\`.

- gene:

  Character. Gene ID for haplotype boxplots.

- ...:

  Additional arguments passed to plotting routines.

## Value

Invisibly, the return value of the dispatched plotting helper.

## Examples

``` r
x <- structure(list(), class = "hbr_run")
plot(x, type = "ld_decay")
#> LD decay plotting selected.
```
