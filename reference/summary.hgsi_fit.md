# Summarise an hgsi_fit object

Summarise an hgsi_fit object

## Usage

``` r
# S3 method for class 'hgsi_fit'
summary(object, ...)
```

## Arguments

- object:

  An \`hgsi_fit\` object.

- ...:

  Ignored.

## Value

\`object\`, invisibly. \#' Summarise an hgsi_fit object

\`object\`, invisibly.

## Examples

``` r
fit <- structure(
  list(traits = "YLD",
       evaluation_label = c(YLD = "honest_discovery_in_fold"),
       model_used = c(YLD = "gblup"),
       ids = sprintf("IND%02d", 1:5),
       parents = data.frame(id = sprintf("IND%02d", 1:5), index = 5:1),
       cv_summary = data.frame(trait = "YLD", method = "M0", r = 0.5),
       cv_compare = data.frame(trait = "YLD", method = "M3",
                               baseline = "M0", mean_diff = 0.01),
       warnings = character(0),
       output_dir = tempdir()),
  class = c("hgsi_fit", "list"))
summary(fit)
#> <hgsi_fit>
#>   traits       : YLD
#>   evaluation   : YLD=honest_discovery_in_fold
#>   models       : YLD=gblup
#>   n individuals: 5
#>   parents      : 5 ranked
#>   fit file     : /tmp/RtmpkEJRPy/hgsi_fit.rds
#> 
#> Cross-validation summary:
#>  trait method   r
#>    YLD     M0 0.5
#> 
#> Comparisons:
#>  trait method baseline mean_diff
#>    YLD     M3       M0      0.01
#> 
#> Top 10 parents:
#>      id index
#> 1 IND01     5
#> 2 IND02     4
#> 3 IND03     3
#> 4 IND04     2
#> 5 IND05     1
```
