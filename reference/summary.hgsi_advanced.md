# Summarise an hgsi_advanced object

Prints the console summary from \[print.hgsi_advanced()\] followed by
the cross-validation summary table, the paired comparisons, the top ten
ranked parents and, when available, the top ten crosses.

## Usage

``` r
# S3 method for class 'hgsi_advanced'
summary(object, ...)
```

## Arguments

- object:

  An \`hgsi_advanced\` object.

- ...:

  Ignored.

## Value

\`object\`, invisibly.

## Examples

``` r
x <- structure(
  list(evaluation_label = c(YLD = "honest_discovery_in_fold"),
       traits = "YLD",
       model_used = c(YLD = "gblup"),
       ids = sprintf("IND%02d", 1:5),
       parents = data.frame(id = sprintf("IND%02d", 1:5), index = 5:1),
       crosses = data.frame(parent_a = "IND01", parent_b = "IND02",
                            uc = 1.2),
       cv_summary = data.frame(trait = "YLD", method = "M0", r = 0.5),
       cv_compare = data.frame(trait = "YLD", method = "M3",
                               baseline = "M0", mean_diff = 0.01),
       map_source = "bundled rice map",
       warnings = character(0),
       output_dir = tempdir()),
  class = c("hgsi_advanced", "list"))
summary(x)
#> <hgsi_advanced>
#>   evaluation   : YLD=honest_discovery_in_fold
#>   traits       : YLD
#>   models       : YLD=gblup
#>   n individuals: 5
#>   parents      : 5 ranked
#>   crosses      : 1
#>   map source   : bundled rice map
#>   output       : /tmp/RtmpMVtYZB
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
#> 
#> Top 10 crosses:
#>   parent_a parent_b  uc
#> 1    IND01    IND02 1.2
```
