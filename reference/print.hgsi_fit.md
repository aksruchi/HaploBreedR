# Print an hgsi_fit object

Print an hgsi_fit object

## Usage

``` r
# S3 method for class 'hgsi_fit'
print(x, ...)
```

## Arguments

- x:

  An \`hgsi_fit\` object.

- ...:

  Ignored.

## Value

\`x\`, invisibly. \#' Print an hgsi_fit object

\`x\`, invisibly.

## Examples

``` r
fit <- structure(
  list(traits = "YLD",
       evaluation_label = c(YLD = "honest_discovery_in_fold"),
       model_used = c(YLD = "gblup"),
       ids = sprintf("IND%02d", 1:5),
       parents = data.frame(id = sprintf("IND%02d", 1:5), index = 5:1),
       warnings = character(0),
       output_dir = tempdir()),
  class = c("hgsi_fit", "list"))
print(fit)
#> <hgsi_fit>
#>   traits       : YLD
#>   evaluation   : YLD=honest_discovery_in_fold
#>   models       : YLD=gblup
#>   n individuals: 5
#>   parents      : 5 ranked
#>   fit file     : /tmp/RtmpRQ6mau/hgsi_fit.rds
```
