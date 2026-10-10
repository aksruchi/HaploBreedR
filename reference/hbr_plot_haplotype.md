# Plot haplotype boxplot with summary table

Draws a two-panel figure: a haplotype boxplot (with jittered points,
mean +/- SE overlay, and post-hoc letters) and a haplotype summary table
(N, frequency, per-SNP alleles, mean/SE, superior marker). The function
has two modes: \*\*pipeline mode\*\* (supply \`gene_id\` +
\`hap_data\` + \`test_res\`) and \*\*CSV mode\*\* (supply \`gene_csv\`
or \`gene_data\` + optional individuals/genotype files).

## Usage

``` r
hbr_plot_haplotype(
  gene_id = NULL,
  hap_data = NULL,
  test_res = NULL,
  trait_col = "trait",
  output_dir = NULL,
  superior_info = NULL,
  functional_snps_used = NULL,
  adjusted_p = NA_real_,
  aa_full_names = TRUE,
  formats = c("pdf", "tiff", "png"),
  gene_list = NULL,
  gene_data = NULL,
  individuals_csv = NULL,
  individuals_data = NULL,
  geno_file = NULL,
  geno_matrix = NULL,
  geno_format = NULL,
  plink_path = "plink",
  gene_csv = NULL
)
```

## Arguments

- gene_id:

  Gene ID (pipeline mode).

- hap_data:

  Test objects from the pipeline (pipeline mode).

- test_res:

  Test results from the pipeline (pipeline mode).

- trait_col:

  Trait column name.

- output_dir:

  Output directory. \`NULL\` writes to the working directory.

- superior_info:

  Superior-haplotype info (pipeline mode).

- functional_snps_used:

  SNPs used (pipeline mode).

- adjusted_p:

  Optional FDR-adjusted p-value.

- aa_full_names:

  Use three-letter amino-acid codes.

- formats:

  Output formats. Any of \`"pdf"\`, \`"png"\`, \`"tiff"\`, \`"svg"\`.

- gene_list:

  Alternative: gene ID (CSV mode).

- gene_data, gene_csv:

  Alternative: in-memory or CSV input (CSV mode).

- individuals_csv, individuals_data:

  Alternative individuals source (CSV mode).

- geno_file, geno_matrix, geno_format:

  Alternative genotype source (CSV mode).

- plink_path:

  Path to PLINK.

## Value

Invisibly, a list with \`plot\` (the composed grob) and \`files\` (named
list of paths written).

## Examples

``` r
toy <- system.file("extdata", "toy", package = "HaploBreedR")
hbr_plot_haplotype(
  gene_list       = "gene1",
  gene_csv        = file.path(toy, "gene1_viz.csv"),
  individuals_csv = file.path(toy, "gene1_individuals.csv"),
  trait_col       = "trait_value",
  output_dir      = tempdir(),
  formats         = "pdf")
#> Warning: for 'gene1 — haplotype summary' in 'mbcsToSbcs': - substituted for — (U+2014)
```
