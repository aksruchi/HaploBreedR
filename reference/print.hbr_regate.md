# Print an \`hbr_regate\` result

Print an \`hbr_regate\` result

## Usage

``` r
# S3 method for class 'hbr_regate'
print(x, ...)
```

## Arguments

- x:

  An object of class \`hbr_regate\`.

- ...:

  Ignored.

## Value

\`x\`, invisibly.

## Examples

``` r
toy <- system.file("extdata", "hgsi_toy", "trait_YLD",
                   package = "HaploBreedR")
if (nzchar(toy) && dir.exists(toy)) {
  run <- hbr_read_results(toy)
  print(hbr_regate(run, alpha = 0.01))
}
#> Re-gated (direction higher): alpha 0.01 | min effect 0.3 | trait threshold none | FDR TRUE
#>   stored call: 2 superior | new call: 2 superior | Jaccard 1
```
