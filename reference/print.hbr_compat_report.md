# Print a genotype-reference compatibility report

Print a genotype-reference compatibility report

## Usage

``` r
# S3 method for class 'hbr_compat_report'
print(x, ...)
```

## Arguments

- x:

  An object of class \`hbr_compat_report\`.

- ...:

  Ignored.

## Value

\`x\`, invisibly.

## Examples

``` r
x <- structure(
  list(status = "PASS",
       summary = data.table::data.table(
         Reference_genome = "TOY", Reference_annotation = "CUSTOM",
         Declared_genotype_build = NA_character_,
         Individuals = 1L, Total_variants = 1L,
         Chromosomes_matched = 1L, Chromosomes_total_reference = 1L,
         Chromosome_match_pct = 100, Valid_position_pct = 100,
         REF_check_coverage = "genome_fasta",
         REF_checked_n = 1L, REF_match_pct = 100,
         Duplicate_positions = 0L, Multiallelic_variants = 0L,
         Reference_mismatches = 0L, Unknown_chromosomes = 0L)),
  class = "hbr_compat_report")
print(x)
#> GENOTYPE-REFERENCE COMPATIBILITY
#> ================================
#> 
#> Reference genome       : TOY (CUSTOM)
#> Declared genotype build: NA
#> Individuals            : 1
#> Total variants         : 1
#> Chromosome match       : 1 / 1 (100.00%)
#> Valid positions        : 100.00%
#> REF check mode         : genome_fasta
#> REF match              : 1 checked, 100.00%
#> Duplicate positions    : 0
#> Multiallelic variants  : 0
#> Reference mismatches   : 0
#> Unknown chromosomes    : 0
#> 
#> STATUS: PASS 
```
