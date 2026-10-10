# Haplotype Pyramiding Probability

Computes the exact joint transmission probability of pyramiding target
loci across chromosomes under linkage.

## Usage

``` r
hbr_pyramid_probability(chr, cm, donor, mating = c("DH", "RIL"))
```

## Arguments

- chr:

  Character or integer vector of chromosome assignments.

- cm:

  Numeric vector of genetic positions (cM).

- donor:

  Integer vector (0/1) indicating parental donor origin.

- mating:

  Character. "DH" or "RIL".

## Value

Numeric. Probability of inheriting all target favorable alleles.

## Examples

``` r
hbr_pyramid_probability(
  chr = c("1", "1", "1"),
  cm = c(10, 10.5, 11),
  donor = c(0, 0, 0),
  mating = "DH")
#> [1] 0.4950373
```
