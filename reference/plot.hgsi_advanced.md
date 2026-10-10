# Plot an hgsi_advanced object

Plot an hgsi_advanced object

## Usage

``` r
# S3 method for class 'hgsi_advanced'
plot(x, type = c("crosses", "cv", "parents"), ...)
```

## Arguments

- x:

  An hgsi_advanced object.

- type:

  Character. \`"crosses"\`, \`"cv"\`, or \`"parents"\`.

- ...:

  Additional arguments passed to the dispatched plotting helper.

## Value

Invisibly, the return value of the dispatched plotting helper.

## Examples

``` r
x <- structure(
  list(crosses = data.frame(
    parent_a = c("A", "B"), parent_b = c("C", "D"),
    mid_index = c(1, 2), uc = c(1.5, 2.5))),
  class = "hgsi_advanced")
plot(x, type = "crosses")
#>   0 of 2 top crosses reordered (max |shift| = 0)
```
