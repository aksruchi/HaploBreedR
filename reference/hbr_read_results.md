# Read finished HaploBreedR results from disk or memory

Loads the output of \[haplobreed_analysis()\] — either the in-memory
result or its output directory — into one object that carries the trait
direction, the effective gate settings, the PCs the run adjusted for
(none if it used no PCs), the tested and superior gene lists, the
functional SNPs per gene, the phenotype table, and the publication-style
results table. \[hbr_advanced_decision()\], \[hbr_regate()\] and
\[hbr_haplotype_blocks()\] consume runs the same way.

## Usage

``` r
hbr_read_results(
  x = NULL,
  trait = NULL,
  phenotypes = NULL,
  phenotype_id_col = "ID",
  gate_params = NULL,
  path = NULL,
  traits = NULL
)
```

## Arguments

- x:

  A \[haplobreed_analysis()\] result, a pipeline output directory, a
  named character vector of directories, or a named list of results.
  \*\*Alternatively\*\*, the legacy arguments \`path\` and \`traits\`
  (see below) are still honoured.

- trait:

  Trait label; default the pipeline's stored \`Trait\`.

- phenotypes:

  Optional wide data.frame (ID column plus one column per trait, plus PC
  columns if the run used PCs). Needed only when the run used PCs and is
  read from files, because \`phenotype_data_used.csv\` does not carry
  the PC columns.

- phenotype_id_col:

  ID column of \`phenotypes\`. Default \`"ID"\`.

- gate_params:

  Optional named list overriding the stored gate settings (\`alpha\`,
  \`min_d\`, \`min_ind\`, \`min_hap_freq\`, \`maf_min\`,
  \`trait_threshold\`, \`require_fdr\`, \`hedges\`). Unspecified entries
  keep the values stored by the pipeline.

- path:

  Legacy alias: a single pipeline output directory.

- traits:

  Legacy alias: a named character vector of pipeline output directories,
  one element per trait.

## Value

An object of class \`hbr_run\` (a list), or a named list of them classed
as \`hbr_run_list\`. Elements of a run:

- \`trait\`, \`direction\`, \`mode\`:

  run identity and the trait direction (\`"higher"\` or \`"lower"\`)

- \`gate\`:

  effective gate settings

- \`phenotype\`, \`pcs\`, \`pc_cols\`:

  trait table and PC columns

- \`gene_snps\`:

  functional SNPs per tested gene

- \`tested\`, \`superior\`, \`superior_label\`:

  gene lists

- \`table\`, \`table_source\`:

  publication-style results table and the file it came from

- \`summary\`, \`pipeline_summary\`:

  the pipeline-summary row

## Details

A single pipeline directory or result returns one \`hbr_run\`. A named
character vector of directories or a named list of results returns one
\`hbr_run\` per element, classed as \`hbr_run_list\`.

## See also

\[hbr_regate()\] to re-apply the gate with different settings,
\[hbr_haplotype_blocks()\] to group superior haplotypes into blocks.

## Examples

``` r
toy <- system.file("extdata", "hgsi_toy", "trait_YLD",
                   package = "HaploBreedR")
if (nzchar(toy) && dir.exists(toy)) {
  run <- hbr_read_results(toy)
  run$trait
  length(run$superior)
  head(run$table)
}
#>   Gene_ID Chr N_Functional_SNPs_Final N_Haplotypes         Test   P_value
#> 1  GENE01   1                       3            5 ANOVA+duncan 1.586e-11
#> 2  GENE02   1                       3            5 ANOVA+duncan 2.094e-02
#> 3  GENE03   1                       3            4 ANOVA+duncan 1.231e-01
#> 4  GENE04   2                       3            4 ANOVA+duncan 2.250e-09
#> 5  GENE05   2                       3            5 ANOVA+duncan 1.504e-03
#> 6  GENE06   2                       3            4 ANOVA+duncan 3.220e-01
#>   Superior_Haplotype Superior_NT_Seq Superior_Mean Cohens_d Second_Haplotype
#> 1               Hap2           2-2-0        51.516    0.075             Hap4
#> 2               Hap1           2-0-0        50.548    0.098             Hap4
#> 3               Hap4           2-2-0        49.973    0.035             Hap1
#> 4               Hap3           0-0-2        52.133    0.387             Hap4
#> 5               Hap3           0-2-0        50.767    0.087             Hap4
#> 6               Hap1           0-2-0        49.874    0.006             Hap2
#>   Adjusted_P Permutation_P Is_Superior   gene is_superior
#> 1  1.269e-10      0.001000       FALSE GENE01       FALSE
#> 2  3.351e-02      0.020940       FALSE GENE02       FALSE
#> 3  1.407e-01      0.123100       FALSE GENE03       FALSE
#> 4  8.999e-09      0.001000        TRUE GENE04        TRUE
#> 5  3.009e-03      0.001504       FALSE GENE05       FALSE
#> 6  3.220e-01      0.322000       FALSE GENE06       FALSE
```
