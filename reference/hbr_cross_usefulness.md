# Analytical Cross Usefulness

Computes the Schnell & Utz (1975) Cross Usefulness (UC) and progeny
genetic variance analytically using recombination covariance matrices
(Zhong & Jannink, 2007).

## Usage

``` r
hbr_cross_usefulness(
  S,
  gebv,
  bins,
  w_eff,
  pairs,
  sel_frac = 0.1,
  h_sel = 1,
  mating = c("DH", "RIL")
)
```

## Arguments

- S:

  Array of parental bin sums from \[.hgsi_parent_bin_sums()\].

- gebv:

  Matrix of parental GEBVs (parents x traits).

- bins:

  List from \[.hgsi_make_bins()\].

- w_eff:

  Numeric vector of effective index weights.

- pairs:

  Two-column matrix of parent integer indices.

- sel_frac:

  Numeric. Selected fraction (default 0.1).

- h_sel:

  Numeric. Selection accuracy (default 1).

- mating:

  Character. "DH" or "RIL".

## Value

data.frame with parent indices, mid-parent index, progeny SD, and UC.

## Examples

``` r
set.seed(1)
S     <- array(rnorm(4 * 3 * 2), dim = c(4, 3, 2))
gebv  <- matrix(rnorm(4 * 2), 4, 2)
bins  <- list(chr = c("1", "1", "2"), center = c(5, 15, 8), n = 3)
pairs <- t(combn(4, 2))
hbr_cross_usefulness(S, gebv, bins, w_eff = c(1, 1), pairs = pairs)
#>   a b  mid_index  sd_index       uc
#> 1 1 2  0.2517443 0.6945748 1.470711
#> 2 1 3  0.6722799 1.2110389 2.797633
#> 3 1 4 -0.7159322 2.4036441 3.502423
#> 4 2 3  0.7823484 1.7694382 3.887683
#> 5 2 4 -0.6058636 2.5341602 3.841545
#> 6 3 4 -0.1853280 1.7167660 2.827568
```
