# Summary of an hbr_run object

Summary of an hbr_run object

## Usage

``` r
# S3 method for class 'hbr_run'
summary(object, ...)
```

## Arguments

- object:

  An hbr_run object.

- ...:

  Additional arguments.

## Value

\`object\`, invisibly.

## Examples

``` r
x <- structure(
  list(pipeline_summary = data.frame(
         Trait = "YLD", Direction = "higher",
         Genes_Tested = 8L, Superior_Haplotypes = 2L)),
  class = "hbr_run")
summary(x)
#> <hbr_run: Single-Trait Haplotype Discovery>
#>   Trait       : YLD (higher)
#>   Genes tested: 8
#>   Superior    : 2 genes
```
