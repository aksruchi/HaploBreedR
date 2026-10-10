# Breeding decisions from HaploBreedR output

Convenience wrapper that runs \[hbr_fit_models()\] followed by
\[hbr_cross_design()\] and returns the combined \`hgsi_advanced\`
object. See the two component functions for the full argument
descriptions.

## Usage

``` r
hbr_advanced_decision(
  pipeline_result = NULL,
  pipeline_results = NULL,
  trait_dirs = NULL,
  output_dir = NULL,
  phenotypes = NULL,
  phenotype_id_col = "ID",
  gate_params = NULL,
  min_concordance = 0.6,
  plink_prefix = NULL,
  weights = NULL,
  top_parents = 25L,
  n_cores = 1L,
  seed = 1L,
  verbose = TRUE,
  cv_repeats = 10L,
  cv_folds = 5L,
  top_frac = 0.1,
  min_count = 5L,
  strata = NULL,
  n_strata = 3L,
  strict = TRUE,
  final_model = c("auto", "gblup", "two_kernel"),
  boot = 2000L,
  cM_per_Mb = NULL,
  genetic_map = NULL,
  bin_cM = 1,
  top_crosses = 20L,
  relatedness_max = 0.3,
  mating = c("DH", "RIL"),
  sel_frac = 0.1,
  h_sel = 1,
  cross_rank = c("uc", "blocks", "balanced"),
  haploblock_method = c("recomb", "ld", "fourgamete", "gabriel", "recomb+gabriel",
    "recomb+fourgamete"),
  haploblock_rmax = 0.01,
  haploblock_r2 = 0.5,
  haploblock_ld_max_cM = 3,
  haploblock_max_span_cM = 5,
  haploblock_flank_cM = 1,
  haploblock_max_snps = 400L,
  haploblock_min_gamete = 0.01,
  run_set_selection = TRUE,
  set_size = 8L,
  n_candidates = 60L,
  block_cM = 5
)
```

## Arguments

- pipeline_result:

  A single \[haplobreed_analysis()\] result.

- pipeline_results:

  Named list of results; takes precedence over \`pipeline_result\`.

- trait_dirs:

  Named character vector of pipeline output directories for traits
  without an in-memory result.

- output_dir:

  Directory for \`hgsi_fit.rds\` and the CV CSVs. \`NULL\` or \`NA\`
  writes nothing.

- phenotypes:

  Optional wide data.frame (ID + one column per trait, plus PC columns
  if the pipeline used PCs).

- phenotype_id_col:

  ID column of \`phenotypes\`.

- gate_params:

  Optional gate override list, per trait or shared.

- min_concordance:

  Minimum Jaccard overlap for the replay to count as faithful.

- plink_prefix:

  PLINK prefix; default \`pipeline_summary\$PLINK_Prefix\`.

- weights:

  Named non-negative emphasis per genetic SD.

- top_parents:

  Number of parents reported.

- n_cores:

  Workers for the GRM.

- seed:

  Random seed.

- verbose:

  Print progress.

- cv_repeats, cv_folds:

  Cross-validation settings.

- top_frac:

  Fraction selected for realised gain.

- min_count:

  Minimum training carriers per haplotype indicator.

- strata, n_strata:

  Fold strata, or number of genotype clusters.

- strict:

  Recompute GRM allele frequencies inside each training fold.

- final_model:

  \`"auto"\`, \`"gblup"\` or \`"two_kernel"\`.

- boot:

  Bootstrap resamples for the CV comparison.

- cM_per_Mb, genetic_map, bin_cM:

  Genetic map. See \[hbr_advanced_decision()\].

- top_crosses:

  Number of crosses reported.

- relatedness_max:

  Maximum relatedness between parents of a cross.

- mating:

  \`"DH"\` or \`"RIL"\`.

- sel_frac, h_sel:

  Selection intensity and heritability for usefulness.

- cross_rank:

  How crosses are ordered: \`"uc"\`, \`"blocks"\` or \`"balanced"\`.

- haploblock_method:

  See \[hbr_advanced_decision()\].

- haploblock_rmax, haploblock_r2, haploblock_ld_max_cM,
  haploblock_max_span_cM:

  Map-based / LD block thresholds.

- haploblock_flank_cM, haploblock_max_snps, haploblock_min_gamete:

  SNP-level method settings.

- run_set_selection, set_size, n_candidates, block_cM:

  Set-selection settings.

## Value

An \`hgsi_advanced\` object.

## Examples

``` r
toy <- system.file("extdata", "hgsi_toy", package = "HaploBreedR")
td  <- file.path(toy, "trait_YLD")
fit <- try(hbr_advanced_decision(
  trait_dirs   = c(YLD = td),
  plink_prefix = file.path(toy, "geno_toy"),
  output_dir   = tempdir(),
  cv_repeats   = 1L, cv_folds = 2L, strict = FALSE,
  run_set_selection = FALSE,
  save_plot    = FALSE,
  verbose      = FALSE))
#> Error in hbr_advanced_decision(trait_dirs = c(YLD = td), plink_prefix = file.path(toy,  : 
#>   unused argument (save_plot = FALSE)
```
