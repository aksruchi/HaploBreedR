# Re-apply Superior Haplotype Gates (Sensitivity Analysis)

Re-filters candidate genes across modified significance thresholds
(alpha), effect sizes (Hedges' g), or trait thresholds directly from
stored summary tables.

## Usage

``` r
hbr_regate(
  summary_table,
  alpha = 0.05,
  min_cohens_d = 0.5,
  require_fdr = TRUE,
  trait_threshold = NULL,
  direction = "higher"
)
```

## Arguments

- summary_table:

  data.frame or data.table of tested candidate genes from pipeline
  output.

- alpha:

  Numeric. Significance threshold (default 0.05).

- min_cohens_d:

  Numeric. Minimum effect size threshold (default 0.5).

- require_fdr:

  Logical. Enforce Benjamini-Hochberg FDR correction.

- trait_threshold:

  Optional numeric trait value requirement.

- direction:

  Character. "higher" or "lower".

## Value

Updated summary data.table with recalculated \`Is_Superior\` calls.

## Examples

``` r
summary_table <- data.frame(
  P_value = c(0.001, 0.02, 0.5),
  Cohens_d = c(0.8, 0.4, 0.1))
hbr_regate(summary_table, alpha = 0.05, min_cohens_d = 0.3)
#>    P_value Cohens_d Adjusted_P Significant_FDR Significant_Nominal Is_Superior
#>      <num>    <num>      <num>          <lgcl>              <lgcl>      <lgcl>
#> 1:   0.001      0.8      0.003            TRUE                TRUE        TRUE
#> 2:   0.020      0.4      0.030            TRUE                TRUE        TRUE
#> 3:   0.500      0.1      0.500           FALSE               FALSE       FALSE
```
