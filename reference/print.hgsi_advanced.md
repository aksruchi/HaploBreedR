# Print an hgsi_advanced object

Console summary of a completed \[hbr_advanced_decision()\] or
\[hbr_cross_design()\] run: evaluation labels, traits, models, parent
and cross counts, block and set summaries, genetic-map source and any
warnings recorded during the run.

## Usage

``` r
# S3 method for class 'hgsi_advanced'
print(x, ...)
```

## Arguments

- x:

  An \`hgsi_advanced\` object.

- ...:

  Ignored.

## Value

\`x\`, invisibly.

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
       map_source = "bundled rice map",
       warnings = character(0),
       output_dir = tempdir()),
  class = c("hgsi_advanced", "list"))
print(x)
#> <hgsi_advanced>
#>   evaluation   : YLD=honest_discovery_in_fold
#>   traits       : YLD
#>   models       : YLD=gblup
#>   n individuals: 5
#>   parents      : 5 ranked
#>   crosses      : 1
#>   map source   : bundled rice map
#>   output       : /tmp/RtmpjfR8yM
```
