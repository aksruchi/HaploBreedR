# Build a manuscript-ready multi-sheet Excel workbook from a pipeline run

Reads \`pipeline_result_for_breeding.rds\` and the CSVs written by
\[haplobreed_analysis()\] in the same directory, and writes one Excel
workbook containing up to 18 sheets covering study summary, gene
results, donor tables, breeding decisions, and annotation.

## Usage

``` r
hbr_build_manuscript_tables(
  rds_file = NULL,
  output_dir = NULL,
  output_file = NULL,
  phenotype_data = NULL,
  id_col = "ID",
  profile = c("manuscript", "supplementary", "full"),
  include_sheets = NULL,
  exclude_sheets = NULL,
  overwrite = TRUE,
  verbose = TRUE
)
```

## Arguments

- rds_file:

  Path to \`pipeline_result_for_breeding.rds\`. Required.

- output_dir:

  Directory holding the pipeline CSVs. \`NULL\` uses
  \`dirname(rds_file)\`.

- output_file:

  Path to the Excel workbook. \`NULL\` auto-names to
  \`\<trait\>\_manuscript_tables.xlsx\` in \`output_dir\`.

- phenotype_data:

  Optional phenotype table.

- id_col:

  ID column in \`phenotype_data\`.

- profile:

  One of \`"manuscript"\`, \`"supplementary"\`, \`"full"\`.

- include_sheets:

  Character vector of sheet names to include.

- exclude_sheets:

  Character vector of sheet names to exclude.

- overwrite:

  Overwrite \`output_file\` if it exists.

- verbose:

  Print progress.

## Value

Invisibly, a list with \`file\`, \`sheets\`, \`skipped\`.

## Examples

``` r
res <- structure(
  list(
    traits = list(GY = list(
      name      = "GY",
      source    = "toy",
      trait_col = "GY",
      direction = "higher",
      info      = list(
        source         = "toy",
        rds_path       = NULL,
        trait_col      = "GY",
        direction      = "higher",
        mode           = "GWAS",
        genes_tested   = 10L,
        superior_count = 2L,
        n_perm         = 1000L,
        ld_decay_bp    = NA_real_))),
    parents  = data.frame(rank = 1L, id = "IND01", index = 0.5,
                          SE = 0.1, P_top15 = 0.9, haplo_cov = 0.8,
                          mean_rel = 0.1, n_crosses = 2L,
                          action = "advance"),
    crosses  = data.frame(rank = 1L, p1 = "IND01", p2 = "IND02",
                          mid_index = 0.4, relatedness = 0.1,
                          complement = 0.5, score = 1.4),
    evidence = data.frame(trait = "GY", direction = "higher",
                          mode = "GWAS", tested = 10L,
                          superior = 2L, n_obs = 100L,
                          sigma2_g = 0.5, sigma2_e = 0.5,
                          h2 = 0.5, w_hat = 0.3, n_features = 5L),
    G            = list(G = diag(1), n_total = 5L, n_used = 5L),
    fits         = list(GY = list(ids = "IND01",
                                  g_M0 = 0.1, g_M2 = 0.1,
                                  rel_M2 = 0.8, sigma2_g = 0.5)),
    weights      = c(GY = 1),
    directions   = c(GY = "higher"),
    output_dir   = tempdir(),
    plink_prefix = "toy",
    maf_min      = 0.05,
    parameters   = list(relatedness_max = 0.3,
                        cv = list(folds = 3L,
                                  repeats = 1L,
                                  n_perm = 50L)),
    sup_sets     = list(),
    index        = data.frame(id = "IND01", index = 0.5,
                              SE = 0.1, rank = 1L,
                              P_top15 = 0.9),
    pipeline_summary = data.frame(
      Trait               = "GY",
      Direction           = "higher",
      Mode                = "GWAS",
      Genes_Tested        = 10L,
      Superior_Haplotypes = 2L,
      LD_Decay_bp         = NA_real_,
      Output_Dir          = tempdir(),
      stringsAsFactors    = FALSE)),
  class = c("hgsi_result", "list"))

rds <- file.path(tempdir(), "fake_result.rds")
saveRDS(res, rds)
suppressWarnings(
  hbr_build_manuscript_tables(
    rds_file    = rds,
    output_file = file.path(tempdir(), "tables.xlsx")))
#> 
#> ====================================================================
#> MANUSCRIPT TABLES
#> ====================================================================
#>   RDS   : /tmp/RtmpVspFCk/fake_result.rds 
#>   Dir   : /tmp/RtmpVspFCk 
#>   Out   : /tmp/RtmpVspFCk/tables.xlsx 
#>   Trait : GY 
#>   Profile: manuscript 
#> 
#>   [Study_Summary           ] skipped: no data
#>   [Superior_Genes          ] skipped: no data
#>   [Superior_Haplotypes     ] skipped: no data
#>   [All_Tested_Genes        ] skipped: no data
#>   [Gene_Attrition          ] skipped: no data
#>   [Parents_Ranked          ] skipped: no data
#>   [Cross_Predictions       ] skipped: no data
#>   [Haplotype_Blocks        ] skipped: no data
#>   [Selected_Parents_Blocks ] skipped: no data
#>   [Cross_Validation        ] skipped: no data
#>   [GO_Enrichment           ] skipped: no data
#>   [Subpop_Haplotype_Freq   ] skipped: no data
```
