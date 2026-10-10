# Print an individual-ID match report

Print an individual-ID match report

## Usage

``` r
# S3 method for class 'hbr_id_report'
print(x, ...)
```

## Arguments

- x:

  An object of class \`hbr_id_report\`.

- ...:

  Ignored.

## Value

\`x\`, invisibly.

## Examples

``` r
rep <- structure(
  list(status = "PASS",
       summary = data.table::data.table(
         N_phenotyped              = 3L,
         N_genotyped               = 2L,
         N_matched                 = 2L,
         N_phenotype_only          = 1L,
         N_genotype_only           = 0L,
         Overlap_pct_of_phenotyped = 66.67),
       matched_ids        = c("a", "b"),
       phenotype_only_ids = "c",
       genotype_only_ids  = character(0),
       id_cleaning_changed = data.table::data.table(
         Original = character(0),
         Cleaned  = character(0))),
  class = "hbr_id_report")
print(rep)
#> INDIVIDUAL ID MATCH REPORT
#> ==========================
#> 
#> Phenotyped individuals  : 3
#> Genotyped individuals   : 2
#> Matched                 : 2 (66.7% of phenotyped)
#> Phenotype-only          : 1
#> Genotype-only           : 0
#> 
#> STATUS: PASS 
```
