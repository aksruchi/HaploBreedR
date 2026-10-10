# Plot a haplotype network for one or more genes

Renders a minimal spanning graph of a gene's haplotypes: nodes sized by
frequency, edges drawn when two haplotypes differ by exactly one SNP.
Optionally highlights and labels the superior haplotype.

## Usage

``` r
hbr_plot_haplotype_network(
  gene_list,
  output_dir = NULL,
  summary_csv = NULL,
  per_gene_dir = NULL,
  result = NULL,
  reference = NULL,
  gff3_path = NULL,
  trait_col = "NT",
  n_gene = NULL,
  sort_by = c("Cohens_d", "Superior_Mean"),
  colour_by_superior = TRUE,
  label_superior = TRUE,
  layout = c("circle", "grid"),
  node_scale = 1,
  palette = "haplobreed",
  theme = "haplobreed",
  width = 8,
  height = 7,
  formats = c("pdf", "png"),
  combined_pdf = TRUE,
  figures_dir = "figures",
  verbose = TRUE
)
```

## Arguments

- gene_list:

  IDs, CSV path, directory path, or data.frame.

- output_dir:

  Directory holding per-gene files.

- summary_csv:

  Optional path to the summary CSV.

- per_gene_dir:

  Override for the directory holding per-gene files.

- result:

  Optional in-memory \[haplobreed_analysis()\] output.

- reference:

  Optional \`hbr_reference\` object.

- gff3_path:

  Optional GFF3 path; parsed once and cached for the session.

- trait_col:

  Trait column name.

- n_gene:

  Keep at most this many genes.

- sort_by:

  Character vector of columns to rank by.

- colour_by_superior:

  Highlight the superior node.

- label_superior:

  Label the superior node.

- layout:

  \`"circle"\` or \`"grid"\`.

- node_scale:

  Multiplier for maximum node radius.

- palette:

  One of \[hbr_palette_names()\].

- theme:

  One of \[hbr_theme_names()\].

- width, height:

  Figure dimensions in inches.

- formats:

  Output formats.

- combined_pdf:

  Also write a multi-page PDF.

- figures_dir:

  Subdirectory of \`output_dir\` for figures.

- verbose:

  Print progress.

## Value

Invisibly, a list with \`plots\`, \`files\`, \`missing_genes\`,
\`combined_pdf\`.

## Examples

``` r
toy <- system.file("extdata", "toy", package = "HaploBreedR")
hbr_plot_haplotype_network(
  gene_list    = "gene1",
  output_dir   = tempdir(),
  per_gene_dir = toy,
  trait_col    = "trait_value",
  formats      = "pdf",
  combined_pdf = FALSE,
  verbose      = FALSE)
#> Warning: for '2 haplotypes • superior = Hap1' in 'mbcsToSbcs': . substituted for • (U+2022)
#> Warning: for 'gene1 — haplotype network' in 'mbcsToSbcs': - substituted for — (U+2014)
```
