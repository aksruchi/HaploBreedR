# Print an hbr_genotype object

Print an hbr_genotype object

## Usage

``` r
# S3 method for class 'hbr_genotype'
print(x, ...)
```

## Arguments

- x:

  An object of class \`hbr_genotype\`.

- ...:

  Ignored.

## Value

\`x\`, invisibly.

## Examples

``` r
g <- structure(
  list(genotypes      = matrix(c(0, 1, 2), nrow = 1),
       variants       = data.frame(SNP = "s1", CHR = "1",
                                   POS = 100, REF = "A", ALT = "T"),
       individuals    = "ind1",
       source_format  = "PLINK",
       source_path    = NA_character_,
       declared_build = NA_character_,
       n_individuals  = 1L,
       n_variants     = 1L,
       streaming      = FALSE),
  class = "hbr_genotype")
print(g)
#> <hbr_genotype> PLINK | in-memory 
#>   Individuals: 1  Variants: 1 
#>   Source: NA 
```
