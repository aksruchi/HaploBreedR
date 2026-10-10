# Population Size for Recombinant Recovery

Calculates the number of plants required to recover at least one
pyramided genotype at 95 percent confidence using Sedcole (1977).

## Usage

``` r
hbr_population_size(p, conf = 0.95)
```

## Arguments

- p:

  Numeric vector of per-plant recovery probabilities.

- conf:

  Numeric. Confidence level (default 0.95).

## Value

Numeric vector of required population sizes.

## Examples

``` r
hbr_population_size(c(0.01, 0.05, 0.10))
#> [1] 299  59  29
```
