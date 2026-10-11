# Print an \`hbr_blocks\` result

Print an \`hbr_blocks\` result

## Usage

``` r
# S3 method for class 'hbr_blocks'
print(x, ...)
```

## Arguments

- x:

  An object of class \`hbr_blocks\`.

- ...:

  Ignored.

## Value

\`x\`, invisibly.

## Examples

``` r
toy <- system.file("extdata", "hgsi_toy", package = "HaploBreedR")
if (nzchar(toy) && dir.exists(toy) &&
    requireNamespace("BEDMatrix", quietly = TRUE)) {
  run <- hbr_read_results(file.path(toy, "trait_YLD"))
  print(hbr_haplotype_blocks(
    run, plink_prefix = file.path(toy, "geno_toy"),
    method = "recomb"))
}
#>   using bundled rice genetic map (Harushima 1998 / RGP); pass `genetic_map = "none"` to disable
#> 2 target haplotypes in 2 blocks (method recomb; map: bundled rice genetic map (Nagamura et al. 1997, n = 1659 markers))
#>  block chr start_cM end_cM n_genes panel_freq
#>  HB001   2      0.0    0.0       1     0.1667
#>  HB002   3      1.1    1.1       1     0.3333
#>   target haplotypes per block: 1: 2 | 2: 0 | 3: 0 | 4: 0 | 5+: 0 
```
