# Multi-Trait Haplotype Breeding Conflicts

Identifies pleiotropic genes where the superior haplotype differs across
distinct breeding traits.

## Usage

``` r
hbr_trait_conflicts(sup_tables)
```

## Arguments

- sup_tables:

  Named list by trait of data.frames with \`gene\` and \`hap\`.

## Value

data.table summarizing pleiotropic concordance or conflict.

## Examples

``` r
sup <- list(
  YLD = data.frame(gene = c("g1", "g2"), hap = c("Hap1", "Hap2")),
  DTF = data.frame(gene = c("g1", "g3"), hap = c("Hap1", "Hap1")))
hbr_trait_conflicts(sup)
#>      gene n_traits  traits haplotypes n_haplotypes         status
#>    <char>    <int>  <char>     <char>        <int>         <char>
#> 1:     g1        2 DTF;YLD       Hap1            1 same_haplotype
```
