# Streamed Genomic Relationship Matrix

Computes the VanRaden (2008) Method 1 genomic relationship matrix in
streaming blocks directly from binary PLINK files.

## Usage

``` r
hbr_build_grm(
  plink_prefix,
  maf_min = 0.05,
  block_cols = 20000L,
  n_cores = 1L,
  verbose = TRUE,
  train_idx = NULL
)
```

## Arguments

- plink_prefix:

  Character. Path prefix to PLINK binary files.

- maf_min:

  Numeric. Minimum minor allele frequency (default 0.05).

- block_cols:

  Integer. SNPs evaluated per memory chunk (default 20,000).

- n_cores:

  Integer. Worker threads for parallel block evaluation.

- verbose:

  Logical. Print progress.

- train_idx:

  Optional integer vector of individuals for allele frequency
  estimation.

## Value

List containing \`A\`, \`d\`, \`p\`, \`keep\`, \`n\`, \`m\`, and
\`snps\`.

## Examples

``` r
toy <- system.file("extdata", "toy", package = "HaploBreedR")
if (requireNamespace("BEDMatrix", quietly = TRUE)) {
  grm <- hbr_build_grm(file.path(toy, "toy"), verbose = FALSE)
  length(grm$snps)
}
#> [1] 50
```
