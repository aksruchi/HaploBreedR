# Spectral Two-Kernel REML

Estimates variance components for a two-kernel mixed model using Kang et
al. (2008) spectral profiling over a convex kernel mixture weight.

## Usage

``` r
hbr_reml_two_kernel(
  y,
  X,
  G_R,
  K_H = NULL,
  w_grid = seq(0, 1, by = 0.1),
  refine = TRUE
)
```

## Arguments

- y:

  Numeric vector of phenotypes.

- X:

  Matrix of fixed-effect covariates.

- G_R:

  Square relationship matrix (background polygenic kernel).

- K_H:

  Square relationship matrix (feature haplotype kernel) or NULL.

- w_grid:

  Numeric grid for kernel mixing weight w in \[0, 1\].

- refine:

  Logical. Perform golden section search refinement around best grid
  point.

## Value

List containing \`w\`, \`s2g\`, \`s2e\`, \`s2R\`, \`s2H\`, and
\`negll\`.

## Examples

``` r
set.seed(1)
n <- 30
X <- cbind(1, rnorm(n))
Z <- matrix(rnorm(n * 20), n, 20)
G <- tcrossprod(Z) / 20
y <- rnorm(n)
hbr_reml_two_kernel(y, X, G)
#> $w
#> [1] 0
#> 
#> $s2g
#> [1] 5.243438e-05
#> 
#> $s2e
#> [1] 1.15485
#> 
#> $s2R
#> [1] 5.243438e-05
#> 
#> $s2H
#> [1] 0
#> 
#> $negll
#> [1] 41.74652
#> 
```
