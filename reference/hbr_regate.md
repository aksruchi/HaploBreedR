# Re-apply the superior-haplotype rule with different settings

The pipeline calls a haplotype superior when four gates pass: a nominal
significance threshold on the trait association (A), a permutation-based
significance threshold (B), an effect-size minimum on the
best-versus-runner-up comparison (C), and — when requested — an absolute
trait value the best haplotype must reach (D). \`hbr_regate()\`
recomputes which genes pass these gates under new thresholds, using the
statistics already stored in the run, and reports how the call changes.

## Usage

``` r
hbr_regate(
  x,
  alpha = NULL,
  min_cohens_d = NULL,
  require_fdr = NULL,
  trait_threshold = NULL,
  direction = NULL,
  ...
)
```

## Arguments

- x:

  A data.frame (legacy) or an \`hbr_run\` (new).

- alpha:

  Significance threshold for the nominal and permutation gates, and for
  Benjamini-Hochberg FDR when \`require_fdr = TRUE\`. \`NULL\` inherits
  the run's stored value.

- min_cohens_d:

  Minimum effect size for gate C. \`NULL\` inherits.

- require_fdr:

  If \`TRUE\`, a gene is superior only if it also passes BH-FDR across
  all tested genes. \`NULL\` inherits.

- trait_threshold:

  Absolute trait value gate D. \`NA\` removes the threshold. \`NULL\`
  inherits.

- direction:

  Kept for backward compatibility with the legacy signature; ignored.
  The run carries its own direction.

- ...:

  Ignored.

## Value

When \`x\` is a data.frame: a \`data.table\` with the recomputed
columns. When \`x\` is an \`hbr_run\`: an object of class \`hbr_regate\`
with elements \`genes\`, \`settings\`, \`overlap\` and \`check\`.

## Details

Two calling conventions are supported.

\*\*Data.frame input.\*\* When \`x\` is a data.frame carrying at least a
\`P_value\` column (and, for the effect-size gate, \`Cohens_d\` or
\`Hedges_g\`), the function returns a copy of the table with
\`Adjusted_P\`, \`Significant_FDR\`, \`Significant_Nominal\` and
\`Is_Superior\` recomputed. This is the legacy behaviour and is fully
backward compatible.

\*\*Run input.\*\* When \`x\` is an \`hbr_run\` (from
\[hbr_read_results()\]) or anything that function accepts, all four
gates are recomputed — including the permutation gate and, when the
pipeline stored a trait threshold, the trait gate. Arguments left at
\`NULL\` inherit the run's stored values, so the default call reproduces
the pipeline exactly. The return is a classed object with the per-gene
calls, the effective settings, the genes gained and lost versus the
stored call, and a Jaccard overlap statistic.

The PCs the pipeline used and the Hedges correction cannot be changed
here, because both alter the stored statistics; re-run the pipeline for
that.

## See also

\[hbr_read_results()\] to build the run input, \[haplobreed_analysis()\]
for the pipeline that produced it.

## Examples

``` r
# Legacy: data.frame input
summary_table <- data.frame(
  P_value  = c(0.001, 0.02, 0.5),
  Cohens_d = c(0.8, 0.4, 0.1))
hbr_regate(summary_table, alpha = 0.05, min_cohens_d = 0.3)
#>    P_value Cohens_d Adjusted_P Significant_FDR Significant_Nominal Is_Superior
#>      <num>    <num>      <num>          <lgcl>              <lgcl>      <lgcl>
#> 1:   0.001      0.8      0.003            TRUE                TRUE        TRUE
#> 2:   0.020      0.4      0.030            TRUE                TRUE        TRUE
#> 3:   0.500      0.1      0.500           FALSE               FALSE       FALSE

# New: hbr_run input re-applies all four gates
toy <- system.file("extdata", "hgsi_toy", "trait_YLD",
                   package = "HaploBreedR")
if (nzchar(toy) && dir.exists(toy)) {
  run <- hbr_read_results(toy)
  rg  <- hbr_regate(run, alpha = 0.01, min_cohens_d = 0.5)
  rg$overlap$gained
}
#> character(0)
```
